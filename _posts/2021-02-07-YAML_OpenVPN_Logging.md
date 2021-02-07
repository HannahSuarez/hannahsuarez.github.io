---
layout: post
title: "Setting up OpenVPN Logging - including YAML Config Snippets"
description: "Setting up OpenVPN Logging - including YAML Config Snippets"
comments: true
keywords: "security, yaml, openvpn, logging, log collection, blueteam"
---

```
input {
  file {
         path => "C:/path/to/openvpn/data.log"
         start_position => "beginning"
    }
}

filter {
  #grok {
    #match => {
      #"message" => "%{SYSLOGBASE} %{USER:user}/%{IP:source_ip}:%{POSINT:source_port} SENT CONTROL \[%{USER:OpenVPNUser}\]: \'%{DATA:msg}\' \(status=%{INT:status_code}\)"
    #}
    #If OpenVPN logs has user details
    #remove_field => ["OpenVPNUser"]

    #match => {
      #"message" => "%{SYSLOGBASE} %{IP:source_ip}:%{POSINT:source_port} SENT #CONTROL \[%{USER:user}\]: \'%{DATA:msg}\' \(status=%{INT:status_code}\)"
    #}
    match => {
    "'%{DATA:msg}'"
    }
  }

  geoip {
    source => "source_ip"
  }

#Add tag for authentication allowed
  if [msg] =~ "PUSH_REPLY" {
    mutate {
      replace => { type => "openvpn_access" }
    }
  }

#Add tag for authentication failed logs
  if [msg] =~ "AUTH_FAILED" {
    mutate {
      replace => { type => "openvpn_err" }
    }
  }

#Add tag for WARNING Logs
  if [msg] =~ "WARNING" {
    mutate {
      replace => { type => "openvpn_warn" }
    }
  }

#should be able to also handle "Apr 7 18:34:54"
#Once the time format is known, change this line
  date {
    match => ["timestamp", "MMM dd HH:mm:ss", "MMM  d HH:mm:ss", "YYYY-MM-DD HH:MM:SS.Z", "YYYY-MM-DD HH:MM:SS Z", "MMM d HH:MM:ss"]
    target => "@timestamp"
  }

  #if "_grokparsefailure" in [tags] {
    #drop { }
  #}
}

output {
  elasticsearch {
    hosts => ["elasticsearch-host:9200"]
    index => "openvpn-%{+YYYY.MM.dd}"
  }
  # debug
  #stdout { codec => rubydebug }
}

  beats {
    port => xxx
  }
```

== Audit Logging

Deploy file integrity monitoring of the following critical locations, but will ultimately depend on where configs are placed.

```
#Linux server config example
/etc/openvpn/server.conf

#Client config files example
<client name/>.conf

#Windows config files example
C:\Program Files\OpenVPN\config\*
```

> YMMV! Your mileage may vary.
