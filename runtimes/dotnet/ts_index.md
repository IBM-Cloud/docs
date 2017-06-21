---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Troubleshooting FAQ
{: #troubleshooting_faq}

**Q**: My application fails to deploy with the message: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  What does this mean?

**A**: If you are receiving a similar message when pushing your application it is most likely caused by your application exceeding either the memory or disk quota limits.  This can be resolved by increasing the quotas for your application.

**Q**: My application fails to deploy with the message: `Failed to compress droplet: signal: broken pipe` or `No space left on device`.  How can I fix this?

**A**: Projects pushed from source code which contain a large number of NuGet package dependencies can sometimes cause this error when the NuGet package cache is enabled.  Set the `CACHE_NUGET_PACKAGES` environment variable to `false` to disable the cache. See the instructions about how to [Disable the NuGet package](diablingNuGet.md) for more information.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
