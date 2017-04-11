---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Memory limits and the Liberty buildpack
{: #memory_limits}

A memory limit must be specified when you deploy an application with the Liberty buildpack.

## Avoid trouble

A "Hello World" servlet that is deployed with the Liberty buildpack with a 256 MB memory limit might not be deployed and run correctly. If it is deployed, it runs close to the 256M limit. Consider specifying a minimum of 512M as the Memory Limit for even simple applications.

## Memory limits and the Liberty buildpack
{: #memory_limits_and_liberty}


When you deploy an application with the Liberty buildpack, you are prompted for a "Memory Limit".

To determine what Memory Limit to specify, it is important to understand that you are not specifying the size of the Java application heap. You are specifying the amount of memory the entire process is able to use. This amount includes the memory that is used by the following components:

* The memory that is used by the warden container.
* The memory that is used to map kernel extensions and system libraries into the process.
* The memory that is used for the jvm executables, jvm working heap, jit space, and compressed references.
* The memory that is used for classes (application server and application), thread stacks, and direct io buffers.
* The memory that is used by the Java application heap.

More information on JVM memory usage can be found at the developerWorks article [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

When you deploy an application, the memory usage of the entire process is monitored. If memory usage exceeds the memory limit that you specified when the application was deployed, the kernel stops the process. This action happens without warning and might be manifested in the following ways:

* If the Memory Limit is exceeded during application deployment, you receive a message that a failure occurred. You might see that the application is flapping. You might see that the application attempted to start multiple times, always unsuccessfully. Or, you might receive a message that indicates the application deployment failed.
* If the Memory Limit is exceeded while the application is in service, the process is stopped. Cloud Foundry attempts to restart the application. The application might restart, but it is unavailable for some amount of time.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
