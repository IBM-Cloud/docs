---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Access Control List

The {{site.data.keyword.SecureGateway}} client provides embedded Accesss Control List (ACL) support. You can allow or restrict (deny) access to on-premises resources by making modifications to the ACL for the client.  This can be done interactively using the client commands or specifying a file that contains the ACLs you want to have in affect.

Starting with v1.5.0, Access Control List rules will be synchronized across all clients connected to the same gateway.  With this, you only need to establish/update your ACL from a single client and it will be shared across all running clients connected to that gateway.  The ACL will also persist across sessions, such that connecting a new client will also apply the same ACL rules.

## Access Control List commands
{: #commands}

The supported ACL commands are:

```
acl allow [<hostname>]:[<port>]
acl deny [<hostname>]:[<port>]
no acl [<hostname>]:[<port>]
no acl
show acl
```
{: screen}

The forms where you have left out either a hostname or port this implies all hostnames or ports.  For example, the following is an ACL rule to allow all hostnames for port 22.

```
acl allow :22
```
{: pre}

The following is another example ACL rule to allow all hostnames for all ports, essentially disabling ACL support. <b>This is not recommended.</b>

```
acl allow :
```
{: pre}

The `show acl` command will show the currently set ACL or provide a message on the overall setting.

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## HTTP/S Route Control using the ACL
{: #routes}

Starting with v1.6.0, HTTP/S destinations can also enforce specific routes on the ACL entries.  These are added the same way as the typical ACL entries, but with the path appended to the end of the rule. For example, the following will allow only requests following the /my/api path to pass through:

```
acl allow localhost:80/my/api
```
{: pre}

With this rule in place, requests to `<cloud host>:<cloud port>/my/api*` will be allowed through.

Routes are only supported on `acl allow` commands.

## Access Control List Precedence
{: #precedence}

After providing an `acl allow :` command, if further `acl allow` commands are entered, the `ALL:ALL` allow rule (from `acl allow :`) will be removed from the list on the assumption that you no longer want to allow unbounded access.  After providing an `acl deny :` command, if another `acl deny` command is entered, the `ALL:ALL` deny rule (from `acl deny :`) will be removed from the list on the assumption that you no longer want to restrict all access.  If you list your current ACL rules via the `show acl` command in the CLI, there will be an indicator to display whether unlisted rules are being allowed or denied.

## Importing an ACL File
{: #import}

You can supply a filename to the `acl file` command that contains the supported ACL commands that will be read by the client upon startup. This file should have commands of the following format:

```
acl allow [<hostname>]:[<port>]
acl deny [<hostname>]:[<port>]
no acl [<hostname>]:[<port>]
no acl
```
{: screen}

<b>Note:</b> `no acl` without any other parameters RESETS the ACL table and sets the access to DENY ALL.

You can find a sample ACL file [here](./securegateway_acl-file.html).

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## Copying your ACL file into the {{site.data.keyword.SecureGateway}} Docker client
{: #docker}

The {{site.data.keyword.SecureGateway}} docker client essentially runs in it's own virtualization container.  The filesystem of the hosting machine is therefore not directly accessible to processes that run inside the container, including the {{site.data.keyword.SecureGateway}} client.  Starting with version 1.8.0 of the Docker Engine, you can use the 'docker cp' command to push files that exist on your host into the container while it is running or stopped.  This must be done in order to use the {{site.data.keyword.SecureGateway}} client's ACL FILE interactive command.

To use the interactive 'cp' support in docker from your host to the docker instance you must be at docker 1.8.0. You can check this using `docker --version`

Once you have done this, your version should display as follows. It is recommended that you allow docker to run as non-root user, so run the command that is suggested after you have upgraded you engine to 1.8.0 or 1.8.2.

```
Client:
 Version:      1.8.2
 API version:  1.20
 Go version:   go1.4.2
 Git commit:   0a8c2e3
 Built:        Thu Sep 10 19:21:21 UTC 2015
 OS/Arch:      linux/amd64

Server:
 Version:      1.8.2
 API version:  1.20
 Go version:   go1.4.2
 Git commit:   0a8c2e3
 Built:        Thu Sep 10 19:21:21 UTC 2015
 OS/Arch:      linux/amd64
```
{: screen}

Then to push out your acl file list to the docker image follow these steps:

- Run 'docker ps' command to find your container ID

```
CONTAINER ID IMAGE                        COMMAND                CREATED        STATUS  PORTS NAMES
764aadce386b ibmcom/secure-gateway-client "node lib/secgwclient" 27 seconds ago Up 26 seconds condescending_nobel
```
{: screen}

- Copy your acl.list using the 'docker cp' command using either the container ID or name:

```
docker cp 01_client.list 764aadce386b:/root/01_client.list
```
{: pre}

- Next, in the {{site.data.keyword.SecureGateway}} client running in docker:

```
cli F /root/01_client.list

 [2015-10-01 08:12:30.091] [INFO] The current access control list is being reset and replaced by the user provided file: /root/01_client.list
 [2015-10-01 08:12:30.093] [INFO] The ACL file process accepts acl allow 127.0.0.1:27017
 [2015-10-01 08:12:30.094] [INFO] The ACL file process accepts acl allow 127.0.0.1:22
```
{: screen}

- Display the ACL:

```
cli> S
 -------------------------------------------------------------------
           -- Secure Gateway Client Access Control List --          

  hostname                               port                  value
  127.0.0.1                             27017                  Allow
  127.0.0.1                                22                  Allow
 -------------------------------------------------------------------
```
{: screen}

Return to [Getting Started - Adding a Client](./securegateway_client.html).
