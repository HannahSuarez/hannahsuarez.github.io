---
layout: post
title: "Thoughts: On grok and dissect (Logstash); and field extractions/field extractor and regular expressions (Splunk)"
description: "Some thoughts working with the two methods for parsing fields in two log management products - Splunk and Logstash (part of Elastic Stack)"
comments: true
keywords: "grok, logstash, elastic search, elk, splunk"
---

I've had a chance of checking out these two - _grok_ (most notably used working with Beats) and _regular expressions_, _field extractions_, _field extractor tool_ (used working with Splunk). This entry covers the basics between the two, it is more like an opinion post (rather than, an article or a how to guide) for anyone that is working with Elastic and/or Splunk about parsing options and just parsing in general..

## grok filter (Elastic)

On Github, there are some helpful [patterns](https://github.com/logstash-plugins/logstash-patterns-core/blob/4ba9bf573583ad510aaf4bd0b3418bdbe3402585/patterns/grok-patterns) that are available and these are built on some common requirements.

Example of a grok pattern:

```
%{IP:client} %{WORD:method} %{URIPATHPARAM:request} %{NUMBER:bytes} %{NUMBER:duration}
```

will produce an output for `123.4.5.6 GET /index.html 555 1.243` with:

```
{
  "client": [
    [
      "123.4.5.6"
    ]
  ],
  "IPV6": [
    [
      null
    ]
  ],
  "IPV4": [
    [
      "123.4.5.6"
    ]
  ],
  "method": [
    [
      "GET"
    ]
  ],
  "request": [
    [
      "/index.html"
    ]
  ],
  "URIPATH": [
    [
      "/index.html"
    ]
  ],
  "URIPARAM": [
    [
      null
    ]
  ],
  "bytes": [
    [
      "555"
    ]
  ],
  "BASE10NUM": [
    [
      "555",
      "1.243"
    ]
  ],
  "duration": [
    [
      "1.243"
    ]
  ]
}
```

The [grok discover](https://grokdebug.herokuapp.com/discover) app is an interesting app to help some already known patterns. I ran the above `GET` example and recieved the same results.

However if you try to run some complicated semi-structured data (for example, an ETW Powershell log in Syslog format):

```
SourceName="Microsoft-Windows-PowerShell" ProviderGuid="{A0C1853B-5C40-4B15-8766-3CF1C58F985A}" EventId="7937" Version="1" ChannelID="17" OpcodeValue="20" TaskValue="102" Keywords="0" EventTime="2019-10-07 15:35:52" ExecutionProcessID="1060" ExecutionThreadID="5152" ActivityID="{5B531820-DB42-0000-E637-535B42DBD401}" EventType="INFO" SeverityValue="2" Severity="INFO" Domain="EC2AMAZ-CM68GLN" AccountName="Administrator" UserID="S-1-5-21-2191890952-3622628201-959830742-500" AccountType="User" ContextInfo="        Severity = Informational__        Host Name = ConsoleHost__        Host Version = 5.1.14393.2636__        Host ID = 564da37d-b66d-45f9-9d71-e1be35b5369d__        Host Application = C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe__        Engine Version = 5.1.14393.2636__        Runspace ID = 444d3657-8c75-46c5-9204-0639475b49b5__        Pipeline ID = 32__        Command Name = Set-StrictMode__        Command Type = Cmdlet__        Script Name = C:\\Program Files\\WindowsPowerShell\\Modules\\PSReadline\\1.2\\PSReadLine.psm1__        Command Path = __        Sequence Number = 242__        User = EC2AMAZ-CM68GLN\\Administrator__        Connected User = __        Shell ID = Microsoft.PowerShell__" Payload="Command Set-StrictMode is Started.__
```
The app will produce an initial pattern like below, were `QS` stands for `Quoted String`:

```
SourceName=%{QS} ProviderGuid=%{QS} EventId=%{QS} Version=%{QS} ChannelID=%{QS} OpcodeValue=%{QS} TaskValue=%{QS} Keywords=%{QS} EventTime=%{QS} ExecutionProcessID=%{QS} ExecutionThreadID=%{QS} ActivityID=%{QS} EventType=%{QS} SeverityValue=%{QS} Severity=%{QS} Domain=%{QS} AccountName=%{QS} UserID=%{QS} AccountType=%{QS} ContextInfo=%{QS} Payload="Command Set-StrictMode is Started.__
```

Even then, it still requires far more massaging of data away from being unstructured

```
{
  "QS": [
    [
      ""Microsoft-Windows-PowerShell"",
      ""{A0C1853B-5C40-4B15-8766-3CF1C58F985A}"",
      ""7937"",
      ""1"",
      ""17"",
      ""20"",
      ""102"",
      ""0"",
      ""2019-10-07 15:35:52"",
      ""1060"",
      ""5152"",
      ""{5B531820-DB42-0000-E637-535B42DBD401}"",
      ""INFO"",
      ""2"",
      ""INFO"",
      ""EC2AMAZ-CM68GLN"",
      ""Administrator"",
      ""S-1-5-21-2191890952-3622628201-959830742-500"",
      ""User"",
      ""        Severity = Informational__        Host Name = ConsoleHost__        Host Version = 5.1.14393.2636__        Host ID = 564da37d-b66d-45f9-9d71-e1be35b5369d__        Host Application = C:\\\\Windows\\\\System32\\\\WindowsPowerShell\\\\v1.0\\\\powershell.exe__        Engine Version = 5.1.14393.2636__        Runspace ID = 444d3657-8c75-46c5-9204-0639475b49b5__        Pipeline ID = 32__        Command Name = Set-StrictMode__        Command Type = Cmdlet__        Script Name = C:\\\\Program Files\\\\WindowsPowerShell\\\\Modules\\\\PSReadline\\\\1.2\\\\PSReadLine.psm1__        Command Path = __        Sequence Number = 242__        User = EC2AMAZ-CM68GLN\\\\Administrator__        Connected User = __        Shell ID = Microsoft.PowerShell__""
    ]
  ],
(AND SO ON...)
```

So as you can see, it hasn't parsed the important information. `Grok` is seen as more suitable when the logs varies for each line ([source](https://github.com/logstash-plugins/logstash-filter-dissect/tree/v1.2.0)).  A case for this is `/var/auth.log` or `/var/message` type of logs which can hold different unstructured information (hint - for `/var/auth.log`, the grok pattern is merely `%{SYSLOGLINE}`).

But still, even with `grok` there is still a need to further structure the unstructured logs.

## dissect filter (Elastic)

There is also the `dissect` filter but it should be noted that it has not been updated for a while, according to the changelog and it is not clear as to what the project status is. I personally haven't used dissect so this info is second-hand.

Example from an Elastic support thread:

```
%{date_stamp} %{+time_stamp} CEF:%{v}|%{vendor}|%{product}|%{version}|%{id}|%{name}|%{severity}|%{extensions}
```

`Dissect` is touted as an option to use for when the line structure tends to be repeated in a reliable manner. A case is the above where the administrator knows that the data is being delivered in CEF (Common Event Format) over Syslog.

## regular expression (Splunk)

At the time of data ingestion, Splunk will then automatically index the data. It is out of scope for this entry to talk about data inputs, but their documentation is very extensive in that area. This is because settings such as data inputs, selecting the data source type, and so on will definitely impact how the data is indexed in Splunk.

When Splunk ingests data, it will automatically identify any fields from the log data source and then it will try to match the existing key/value pair fields (another writer touts this as 'intelligence' but this is a fairly basic attribute in log management dashboards). How the data matches will depend on how the data source is set up but is out of scope in this post. This is done at the time of index. As it ingests the data, it will then convert it to events (since, timestamped data can be indexed).

Regular expressions are used to match patterns and for extracting fields. You can read more at their documentation [here](https://docs.splunk.com/Documentation/Splunk/7.3.1/Knowledge/AboutSplunkregularexpressions).

Note that regular expressions, of which Splunk uses, has a different format. See simple example below:

```
^(?:[^\n]*}){1}
```

In this case with regular expressions you explicitly state the rules of the expressions, where Elastic's preference for grok is more around patterns.

By the way, _regular expressions_ should not be confused with _regex_ in Splunk. The regex command is used to remove results that do not match the specified regular expressions in Splunk.

## field extractions and the field extractor (Splunk)

Splunk offers a visual aide called the [field extractor](https://docs.splunk.com/Documentation/Splunk/7.3.1/Knowledge/ExtractfieldsinteractivelywithIFX) which can offer two field extraction methods: regular expression and delimiters. Note that it does not include grok pattern creation, however, Elastic's `dissect` filter does implement delimiters.

The field extractor is very handy for admins working with various log data sets and need a way to build the regular expression or comma delimited format. One thing I found, using the webtool mid this year, has been how seemingly sluggish it is to use. However it may be my Windows EC2 instance.

Another interesting thing about this tool is that you can extract data based on uploaded data like a CSV file.

Once the fields are noted for extraction, you create a new field and then build the regular expression around it to build a new index in Splunk.

## Extra notes to consider

**Elastic moves fast and is open source**

Another note to keep in mind is that, in this constantly evolving space new features are constantly being announced and published. Elastic is certainly one of them. For example, the Logstash component of the Elastic Search, Logstash, Kibana (ELK) trifecta, should no longer be referred to ELK. This is because Beats, a lightweight data shipper from Elastic, sits between the data source and Logstash. Not only that, but before _grok_ filter ([source here](https://github.com/logstash-plugins/logstash-filter-grok)), there was the _dissect_ filter which has not been updated for [more than two years](https://github.com/logstash-plugins/logstash-filter-dissect/tree/master) as of writing. Therefore your mileage will vary. It takes time and resources for administrators to roll-out logging, let alone be versed in the latest schema or filters.

**Splunk offers more than just log management**

If you are not already aware of Splunk, they are more than just log management and offer a suite of products such as Splunk Enterprise Security which is a SIEM suite. They also have a SOAR (security orchestration, automation and response) platform and form, making them the choice for those looking for a solution beyond log collection.

**Security / SIEM products**

The first time I have come across Splunk was back in 2015 when they had a hackathon. Back then, I more or less associated them with analytics, big data, and less on security. However, with a series of acquisitions (ie Caspida, a cybersecurity startup, in 2015), partnerships and alliances as well as product moves they have rightfully set themselves as top of mind for people looking for security solutions as well.

Therefore, Splunk has had a far longer lead time than Elastic when it comes to developing the security products and inside know-how for security. Elastic, though, has the leverage of having both a corporate and community (due to the open source modules) base for outreach when it comes to promoting the launch of their Elastic SIEM.

## But wait, there's more...*

The, what should be, simple job of shipping data from the source to the server (for processing, indexing, etc) should be simple enough. However, it is not so. Splunk users are most likely using _Splunk Forwarders_ and Elastic users are most likely using _Logstash/Beats_. This encourages a form of vendor inertia unless administrators decide that it is time to look beyond and consider other solutions, _in addition to their own provider_ to fill the gaps in their log shipping problems. This is where vendor-neutral solutions come in, for example [NXLog](https://www.nxlog.co) a project that I am involved in, is one such solution. There are others on the market that can plug into Splunk or be a part of the Elastic platform (in this case, Elastic and Kibana) to extend or fill any gaps in collection.

> Your mileage may vary.
