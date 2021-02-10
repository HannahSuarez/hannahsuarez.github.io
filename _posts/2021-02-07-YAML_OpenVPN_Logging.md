---
layout: post
title: "Setting up OpenVPN Logging - including YAML Config Snippets"
description: "Setting up OpenVPN Logging - including YAML Config Snippets"
comments: true
keywords: "security, yaml, openvpn, logging, log collection, blueteam"
---

**Example Windows**

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
    #If OpenVPN logs contain user details
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
  # stdout { codec => rubydebug }
}

  beats {
    port => xxx
  }
```

> The above sample is not written by me. Alas I have not been able to yet find the origins of this, as it has been residing in my files but happy to reference the source once I can.


**Audit Logging**

Deploy file integrity monitoring of the following critical locations, but will ultimately depend on where configs are placed.

Where to obtain OpenVPN log file for...

**Linux:**

The OpenVPN log file is defined on the `/etc/openvpn/server.conf`.
The verbosity of the log is also defined in the `server.conf` file.

There will also be authentication process, such as preauthorization, authentication, enrolment events, and messages stating in `“/var/log/messages”` in addition to the OpenVPN log file.

**Windows**

Potential paths include `\Program Files\OpenVPN\log` and `C:\Program Files\OpenVPN\config\`

```
#Linux server config example
/etc/openvpn/server.conf

#Client config files example
<client name/>.conf

#Windows config files example
C:\Program Files\OpenVPN\config\*
```

**OpenVPN Config Tests**

* Load the log sample and change the input path to the right location.
* When a user successfully authenticates, a type is created `“openvpn_access”`
* When a user does not successfully authenticates, a type is created `“openvpn_err”`.
* Reload the configuration and check that Elastic does not reindex the event.
* Change the OpenVPN configuration on the client and see if it triggers a file integrity monitoring event.
* Change the OpenVPN configuration on the server and see if it triggers a file integrity monitoring event.
* Windows -> Client connects to OpenVPN server (message is logged with type `"openvpn_access"`), then successful log in (Event ID `4624`) is then logged.

> YMMV! Your mileage may vary.
