---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# About customizing NuGet package sources
{: #customizing_nuget}
You can use the NuGet.Config file in the application's root directory to control where the application downloads dependencies. In the following example, configuring the `<packageSources>` property defines any keys and API URLs for the application to retrieve packages.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
