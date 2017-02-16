---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Viewing logs from the Bluemix CLI
{: #logging_containers_cli}

You can review logs in the CLI for the containers that you are running on Bluemix.
{:shortdesc}



{{site.data.keyword.Bluemix_notm}}

Viewing container logs is useful for analyzing why a container stopped or reviewing container output. However, cf ic logs can be used only if the app writes logs to the STDOUT and STDERR output streams. Because the CLI does not use the logging service, you cannot view logs that you specify with environment variables. If you create your apps to write to these standard output streams, you can view container logs via the command line even if the container shuts down or crashes.

    Optional: Run an example container that generates log output. This command runs a container that repeats "Hello World" every 5 seconds.

    cf ic run --name example_log_container registry.stage1.eu-gb.bluemix.net/ibmliberty bash -c 'while sleep 5; do echo "Hello World"; done'

    List your container to view its status.

    cf ic ps

    CONTAINER ID        IMAGE                                               COMMAND                  CREATED             STATUS                   PORTS               NAMES
    6fcf69aa-785        registry.stage1.eu-gb.bluemix.net/ibmliberty:latest           "bash -c while sleep "   32 seconds ago      Running a second ago                         example_log_container

    This command also shows individual instances of a container group. To confirm which instances are associated with a particular group, run cf ic group instances GROUPNAME.
    View the logs of the container Use the -t flag to display the timestamp and the -f flag to follow the container's running log output.

    cf ic logs -t -f example_log_container

    +2016-12-08T19:49:31.307854194Z Hello World
    +2016-12-08T19:49:36.308732957Z Hello World
    +2016-12-08T19:49:41.309584275Z Hello World
    +2016-12-08T19:49:46.310452464Z Hello World
    +2016-12-08T19:49:51.311398846Z Hello World
    +2016-12-08T19:49:56.312385701Z Hello World

    Quit the log flow with CTRL+c

    +2016-12-08T19:51:06.325924148Z Hello World
    +2016-12-08T19:51:11.326833396Z Hello World
    +2016-12-08T19:51:16.327732363Z Hello World
    ^C
    $ 

    Stop and remove the container to prevent it from consuming resources.

    cf ic stop example_log_container

    cf ic rm example_log_container

See docker logs to review all log flags. To learn how to specify more logs, try Tutorial: Testing the logging capabilities.
