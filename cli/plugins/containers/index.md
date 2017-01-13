---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Containers CLI
{: #containercli}

*Version:* 1.0.0

IBM Containers CLI is a {{site.data.keyword.Bluemix_notm}} CLI plug-in to manage containers and container groups on Bluemix.
{: shortdesc}

**Note:** *Prerequisites* list which actions are required before using the command. Commands that have no prerequisite actions list **None**. Otherwise, prerequisites might include one or more of the following actions:
<dl>
<dt>Endpoint</dt>
<dd>An API endpoint must be set through the <code>bluemix api</code> before using the command.</dd>
<dt>Login</dt>
<dd>Login by using the <code>bluemix login</code> command is required before using this command. If logging in with federated ID, use '--sso' option to authenticate with one time passcode.</dd>
<dt>Target</dt>
<dd>The <code>bluemix target</code> command must be used to set an org and space before using this command.</dd>
<dt>Docker</dt>
<dd>Docker CLI (docker) is required to run commands in IBM Containers CLI plugin.</dd>
</dl>

<table summary="bluemix commands that you can use to manage containers on Bluemix.">
<caption>Table 1. Commands for managing containers on Bluemix</caption>
 <thead>
 <th colspan="5">Commands for managing containers on Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

Control a running container or view its output. Use `CTRL+C` to exit and stop the container. This command calls the Docker CLI. For more information, see the [attach ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} command in the Docker help.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>--no-stdin (optional)</dt>
   <dd>Do not include the standard input.</dd>
   <dt>--sig-proxy (optional)</dt>
   <dd>Proxy all received signals to the process. The default value is <i>true</i>.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
    </dl>

<strong>Examples</strong>:

The following example shows a request to attach to the container `my_container`:
```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

Call the IBM Containers build service to build a Docker image locally or in your private {{site.data.keyword.Bluemix_notm}} repository. This command calls the Docker CLI. For more information, see the [build ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} command in the Docker help.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (required)</dt>
   <dd>The repository name to apply to the image that is created.</dd>
   <dt>--no-cache (optional)</dt>
   <dd>Do not use the cache when the image is built. The default is <i>false</i>.</dd>
   <dt>--pull (optional)</dt>
   <dd>Attempt to pull the base image from the registry even if it is cached.</dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Suppress the verbose output that is generated by the containers. The default is <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (required)</dt>
   <dd>The path to the Dockerfile and context on the local host.</dd>
    </dl>

<strong>Examples</strong>:

The following example shows a request to build an image that is named *myimage*. The Dockerfile and other artifacts to be used in the build are in the same directory that the command is running from. Because the registry and namespace are included with the image name, the image is built in your organization's private {{site.data.keyword.Bluemix_notm}} repository.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic cp
{: #bluemix_ic_cp}
Copy files or folders between a container and the local filesystem. This command calls the Docker CLI. For more information, see the [cp ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} command in the Docker help.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Access a Docker Hub image or an image from your local registry and copy the image to your private {{site.data.keyword.Bluemix_notm}} repository.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (required)</dt>
   <dd>The source repository and image name.</dd>
   <dt><i>DESTINATION_IMAGE</i> (required)</dt>
   <dd>The private {{site.data.keyword.Bluemix_notm}} repository URL, which includes the namespace and the destination image name. A tag for the image is optional.</dd>
   </dl>

<strong>Examples</strong>:

Copy an image from the source repository to your private repository and add a tag for the image:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copy the `sinatra` image from the `training` repository to your private repository `registry.ng.bluemix.net/mynamespace` and name the image as `mysinatra`. Add a tag `v1` for the image `mysinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

Execute a command within a container. For more information, see the [exec ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} command in the Docker help.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-d|--detach (optional)</dt>
   <dd>Run the specified command in the background.</dd>
   <dt>-it (optional)</dt>
   <dd>Interactive mode. Keep the standard input displaying. Type <i>exit</i> to exit.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (optional)</dt>
   <dd>The user name.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>The command to execute within the container or containers specified.</dd>
   </dl>

<strong>Examples</strong>:

Execute the `bash` command within the `my_container` container in the interactive mode:

```
bluemix ic exec -it my_container bash
```

Execute the `date` command within the `my_container` container:

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Create a scalable container group.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (required)</dt>
   <dd>The image to be included in each container instance in the container group. You can list commands after the image, but do not put any options after the image. Include all options before you specify an image. <br><br>If you use an image in your organization's private {{site.data.keyword.Bluemix_notm}} repository, specify the image in the format: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>If you use an image that is provided by IBM Containers, do not include your organization's namespace. Specify the image in the format: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (required)</dt>
   <dd>Assign a name to the group. <i>-n</i> is deprecated.<br>
   <strong>Tip:</strong> The container name must start with a letter. The name can include uppercase letters, lowercase letters, numbers, periods ., underscores _, or hyphens -.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (optional)</dt>
   <dd>Assign a memory limit to the group in MB. When you create a container group from the CLI, the default value for each container instance is <i>64</i> MB. When you create a container group from the {{site.data.keyword.Bluemix_notm}} Dashboard, the default value for each container instance is <i>256</i> MB. Accepted values are <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> and <i>2048</i>. After a memory limit is assigned, the value can't be changed.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (optional)</dt>
   <dd>The host name, such as <i>mycontainerhost</i>. The host and the domain combine to form the full public route URL, such as <i>http://mycontainerhost.mybluemix.net</i>. When you review the details of a container group with the <i>bluemix ic group-inspect</i> command, the host and the domain are listed together as the route.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>Usually, the domain is <i>.mybluemix.net</i>. The host and the domain are combined to form the full public route URL, such as <i>http://mycontainerhost.mybluemix.net</i>. When you review the details of a container group with the <i>bluemix ic group-inspect</i> command, the host and the domain are listed together as the route.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (optional)</dt>
   <dd>Set the environment variable. List multiple keys separately. If quotation marks are included, include them around both the environment variable name and the value. For example: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  The following table shows some commonly used environment variables that you can specify:</dd>
    </dl>


|  Environment variable                              |     Description                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bind a service to a container. Use the `CCS_BIND_APP` environment variable to bind an app to the container. The app is bound to the target service and acts as a bridge that allows {{site.data.keyword.Bluemix_notm}} to bring your bridge app’s `VCAP_SERVICES` information to the running container instance. For more information about creating a bridge app, see [Binding a service to a container](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | To bind a Bluemix service directly to a container without using a bridge app, use CCS_BIND_SRV. This binding allows Bluemix to inject the VCAP_SERVICES information into the running container instance. To list multiple Bluemix services, include them as part of the same environment variable. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Add a log file to be monitored in the container. Include the `LOG_LOCATIONS` environment variable with a path to the log file. |
{: caption="Table 2. Commonly used environment variables" caption-side="top"}

 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (optional)</dt>
   <dd> Import environment variables from a file where ENVFILE is the path to your file on your local directory. Every line in the file represents one key=value pair. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (optional)</dt>
   <dd>Attach a volume to a container by specifying the details in the format <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: The volume ID or name.</li>
   <li><i>CONTAINER_PATH</i>: The absolute path to the volume in the container.</li>
   <li>ro: Optional. Specifying <i>ro</i> makes the volume read-only instead of the default read/write.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (optional)</dt>
   <dd>Expose the port for the HTTP traffic. Containers in your group must listen to the HTTP port. HTTPS requests can't be made. For container groups, you can't include multiple ports. <br><br>When you specify a port, you make the app available to the {{site.data.keyword.Bluemix_notm}} Load Balancer or containers that are trying to reach the host in the same {{site.data.keyword.Bluemix_notm}} space. Then the {{site.data.keyword.Bluemix_notm}} load balancer or containers can use the port to reach the host and the app in the same {{site.data.keyword.Bluemix_notm}} space. If a port is specified in the Dockerfile for the image that you are using, include that port. <br>
   <strong>Tips</strong>: <ul>
   <li>For the IBM certified Liberty Server image or a modified version of this image, enter port 9080.</li>
   <li>For the IBM certified Node.js image or a modified version of this image, enter port 8000.</li>
   </ul>
   </dd>
   <dt>-P (optional)</dt>
   <dd>Publish all ports</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The minimum number of instances. The default is 1. If you set a minimum number of instances, the value can't be changed after the container group is created.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The maximum number of instances. The default is 2. If you set a maximum number of instances, the value can't be changed after the container group is created.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The number of instances that you require. The default is 2.</dd>
   <dt>--auto (optional)</dt>
   <dd>When the container group is created and the automatic recovery is enabled, IBM Containers check the health of each instance with an HTTP request to the port that is assigned.<br>
   If no response is received from a container instance in 2 subsequent 90 second intervals, the instance is removed and replaced with a new instance. No action is taken if the container is responsive. This process is repeated continuously. During a 30 minute window, if the total number of different containers that are members of the group equals or exceeds 3 times the maximum observed size of the group, the automatic recovery is disabled permanently for the container group. To enable automatic recovery again, you must re-create the container group.</dd>
  <dt>--anti (optional)</dt>
  <dd> Use anti-affinity to make your container group more highly available. The --anti option forces every container instance in your group to be placed on a separate physical compute node, which reduces the chances of all containers in a group crashing due to a hardware failure. You might not be able to use this option with larger group sizes because each Bluemix region and organization has a limited set of compute nodes available for deployment. If your deployment does not succeed, either reduce the number of container instances in the group or remove the --anti option. </dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>The command and arguments that are passed to the container group to execute. This command must be a long-running command. Do not use a short-lived command that does not run for very long, for example, <i>/bin/date</i>, because the short-lived command might cause the container to crash.  <br> <strong>Notes:</strong> <ul>
   <li>The command and its arguments must come at the end of the <i>bluemix ic run</i> command line.</li>
   <li>If the command arguments include the hyphen -, as in <i>-c</i> in the previous example command, the command must be preceded by two hyphens --.</li>
   </ul></dd>
   </dl>


<strong>Examples</strong>:

Create a container group `my_container_group` by using the `registry.ng.bluemix.net/ibmnode` image that is provided by IBM Containers, and then run the `ping localhost` long-running command on that container group:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Create a container group `my_container_group` by using the `registry.ng.bluemix.net/ibmnode` image that is provided by IBM Containers, and then run the `tail -f /dev/null` long-running command on that container group:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Create a scalable group `mygroup` with the automatic recovery enabled by using the `registry.ng.bluemix.net/ibmliberty` image. The port is `9080`, the host name is `mycontainerhost`, the domain name is `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

View detailed information, such as environment variables, ports, or memory, that is specified for a container group when it is created.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to inspect the container group `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

List instances of a specified container group.

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

List all instances of the container group `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Remove a container group from a space.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-f|--force (optional)</dt>
   <dd>Forces the removal of a running or failed container.</dd>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to remove a container group, where `my_group` is the name of the container group.
```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Update a container group.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Tip:** To update the host name or domain for a container group, use `bluemix ic route-map [-n HOST] [-d DOMAIN] CONTAINER_GROUP`.

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
 <dl>
   <dt>--anti (optional)</dt>
   <dd>Use anti-affinity to make your container group more highly available. The --anti option forces every container instance in your group to be placed on a separate physical compute node, which reduces the odds of all containers in a group crashing due to a hardware failure. You might not be able to use this option with larger group sizes because each Bluemix region and organization has a limited set of compute nodes available for deployment. If your deployment does not succeed, either reduce the number of container instances in the group or remove the --anti option.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The number of instances that you require. The default is <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(optional)</dt>
   <dd>Set the environment variable. List multiple keys separately. If quotation marks are included, include them around both the environment variable name and the value. For example: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to update the container group `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

List container groups in the private {{site.data.keyword.Bluemix_notm}} repository of the organization.

```
bluemix ic groups [-q]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
	<dl>
	<dt>-q (optional)</dt>
   	<dd>Only display group IDs</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

View a list of all available images in the organization's private {{site.data.keyword.Bluemix_notm}} repository. For more information, see the [images ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} command in the Docker help. The list includes the image ID, the created date, and the image name.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-a|--all (optional)</dt>
   <dd>Include all of the image layers for each image in your organization's repository, not only the most recent layer.</dd>
   <dt>-f (optional)</dt>
   <dd>Filter the list of images by the condition provided.</dd>
   <dt>--no-trunc (optional)</dt>
   <dd>Do not truncate the output.</dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Display only the numeric IDs.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to receive a list of available images for the organization:
```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

View a set of information that describes the state of the container cloud service instance. The information includes the containers limit, containers usage, containers that are running, memory limit, memory usage, floating IP address limit, floating IP address usage, CCS host URL, registry host URL, and debug mode status.

```
bluemix ic info
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


## bluemix ic init
{: #bluemix_ic_init}

Initialize the containers environment on your local machine to use the full capabilities of the IBM Containers service.

```
bluemix ic init
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

**Note:** Before initialization, ensure that the Docker CLI (docker) is installed and configured in your PATH environment variable. To switch to another region, use the `bluemix region-set` command.

<strong>Examples</strong>:

Switch to the `us-south` region:

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

View the information about a container. For more information, see the [inspect ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} command in the Docker help.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>IMAGE</i> (required)</dt>
   <dd>View detailed information about a specific image by specifying the image name or ID.</dd>
   <dt>images (required)</dt>
   <dd>View detailed information about all of the images in your repository.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>View detailed information about a specific container by specifying the container name or ID.</dd>
   </dl>

**Tip:** Only one of *IMAGE*, *images*, or *CONTAINER* can be specified at a time.

<strong>Examples</strong>:

The following example shows a request to inspect a container that is named `proxy`:
```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Bind an available floating IP address to a container.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (required)</dt>
   <dd>The IP address to be bound.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container ID or name to be bound.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to bind the IP address `192.123.12.12 to` the container `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Release a floating IP address from the container cloud service instance.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (required)</dt>
   <dd>The IP address to release.</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
Request a new floating IP address.

```
bluemix ic ip-request [-q]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-q (optional)</dt>
   <dd>List only the IP addresses, without the IDs for the containers that are bound to those IP addresses.</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Unbind a floating IP address from its container.

Public IP addresses are a limited resource in IBM Containers. Therefore, public IP addresses that are allocated to a space and not bound to a container are periodically reclaimed from free trial users, approximately on a weekly basis. Unbound public IP addresses are never reclaimed from pay as you go or subscription customers.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (required)</dt>
   <dd>The IP address to be unbound.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container ID or name to be unbound.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to unbind the IP address `192.123.12.12` from the container `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

List the available floating IP addresses for the user that is logged. The list includes IP addresses and the container ID that the IP addresses are linked to. If the IP address is unused, no container ID will be shown.

```
bluemix ic ips [-q]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-q (optional)</dt>
   <dd>List only the IP addresses, without the IDs for the containers that are bound to those IP addresses.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to receive a list of all IP addresses for the organization.
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

Stop a running process in a container without stopping the container. For more information, see the [kill ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} command in the Docker help.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (optional)</dt>
   <dd>Send a command to the process that is running in the container.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container ID or name.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to kill the process in a container that is named `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

Show the output or error logs for a running container. For more information, see the [logs ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} command in the Docker help.
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

View the name of the private {{site.data.keyword.Bluemix_notm}} image repository for the organization that you are logged in to.

```
bluemix ic namespace-get
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Set the name of the private {{site.data.keyword.Bluemix_notm}} image repository the organization that you are logged in to.

*Restriction*: You can't use a hyphen `-` in the name of your repository namespace.

```
bluemix ic namespace-set NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>NAME</i> (required)</dt>
   <dd>A one-time only function to set the repository namespace for your organization, if it is not already set. After you set the namespace, reinitialize IBM Containers through `bluemix ic init` command before you continue.</dd>
   </dl>


## bluemix ic pause
{: #pause}

Pause all processes within a running container. For more information, see the [pause ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} command in the Docker help. To stop a container, see the [bluemix ic unpause](#unpause) command.

```
bluemix ic pause CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:
   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Responses</strong>:

- Paused container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to pause a container that is named `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

List port mappings or a specific mapping for the container. This command wraps the `docker port` command. For more information, see the [port ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} command in the Docker help.


## bluemix ic ps
{: #bluemix_ic_ps}
View a list of containers that are running in the logged-in user's namespace. By default, this command shows only containers that are running. For more information, see the [ps ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} command in the Docker help.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-a|--all (optional)</dt>
   <dd>Show all containers, both running and stopped.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (optional)</dt>
   <dd>Search containers that have a specific environment variable value. You can filter your containers by any environment variable key or value that is listed in the Env section of your CLI response when you inspect a container. Replace SEARCH_CRITERIA with the key or value you are looking for. Your search criteria does not need to be an exact match. </dd>
   <dt>-s|--size (optional)</dt>
   <dd>List the sizes of the containers.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (optional)</dt>
   <dd>List the most recently created containers, where <i>NUM</i> is the number of the most recently created containers that you want to return. <br><br> For example, if you created containers <i>node1</i> through <i>node5</i> sequentially, the command <i>bluemix ic ps --limit 2</i> returns node4 and node5 because they are the last two containers that are created. </dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Display only container IDs.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to see all running and stopped containers:
```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
Rename a container. For more information, see the [rename ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} command in the Docker help.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

<dl>
   <dt><i>OLD_NAME</i> (required)</dt>
   <dd>The old name of the container.</dd>
   <dt><i>NEW_NAME</i> (required)</dt>
   <dd>The new name of the container.</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

Re-create the IBM Containers service in the Bluemix space that you are logged into. The original quota for the space is maintained.

<strong>Important</strong>: When you run this command, none of your single containers and groups in this space will be migrated to the re-provisioned space and they will be removed during the migration process.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Command options</strong>:

<dl>
   <dt>--force|-f (optional)</dt>
   <dd>Forces the re-creation of the IBM Containers service in the Bluemix space.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (optional)</dt>
   <dd>The name of IBM Containers availability zone where your containers are deployed. If no availability zone is specified, the default availability zone that is set for the region is used.</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

Restart a container. For more information, see the [restart ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} command in the Docker help.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (optional)</dt>
   <dd>The number of seconds to wait before the container is restarted.</dd>
   </dl>


<strong>Responses</strong>:

- Restarted container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to restart a container that is named `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Remove a container. For more information, see the [rm ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} command in the Docker help.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-f|--force (optional)</dt>
   <dd>Forces the removal of a running or failed container.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Responses</strong>:

- Removed container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service.

<strong>Examples</strong>:

The following example shows a request to remove a container that is named `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Remove an image from the logged-in user's namespace. For more information, see the [rmi ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} command in the Docker help.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (optional)</dt>
   <dd>Change the registry host. The default is to use the registry that you specify in the <i>bluemix ic init</i> command.</dd>
   <dt><i>IMAGE</i> (required)</dt>
   <dd>The name of the image that you want to remove. If a tag is not specified in the image name, the image tagged <i>latest</i> is deleted by default.</dd>
   </dl>

<strong>Responses</strong>:

- Removed: `{IMAGE}`

 Where `{IMAGE}` is the name of the image that was removed.

- Error! No registry host specified.

- Image remove failed - Could not connect to container cloud registry

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

<strong>Examples</strong>:

The following example shows a request to remove the image `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Establish the route for internet traffic to use to access the container group. You can use this command to establish a new route or update an existing route.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (optional)</dt>
   <dd>The host name for the route. The host name is the first part of the full public route URL, such as <i>mycontainerhost</i> in the URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>The domain name for the route, which is the second part of the full public route URL. In most cases, the domain is <i>mybluemix.net</i>. You can also use this parameter to specify a private domain.</dd>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to map the route for the group that is called `GROUP1`, where `my_host` is the host name, `mybluemix.net` is the domain.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Establish the route for internet traffic to use to access the container group. You can use this command to establish a new route or update an existing route.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (optional)</dt>
   <dd>The host name for the route.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>The domain name for the route.</dd>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to unmap the route for the group that is called `GROUP1`, where `my_host` is the host name and `organization.com` is the domain.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic run
{: #bluemix_ic_run}

Start a new container in the container cloud service from an image name. For more information, see the [run ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} command in the Docker help.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Note:** Ensure that the Cloud Foundry command tool is installed and that you have a Cloud Foundry token. Successful login by using `bluemix login` and `bluemix ic init` generates the required token and certificates.


<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>  (optional)</dt>
   <dd>Expose the port for the HTTP traffic. Include any ports that are specified in the Dockerfile for the image that you are using. You can include multiple ports with multiple <i>-p</i> options. Exposing a port will automatically bind a public IP address to the container if a public IP address is available. <br><br>If you have an existing IP address in the space that you want to bind to the container, you can specify the IP address rather than bind it later. The IP address must be specified in the  format: &lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>For more information about requesting IP addresses for a space, see <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> command. <br><br>When you specify a port, you are making the app available to the {{site.data.keyword.Bluemix_notm}} Load Balancer or containers in the same {{site.data.keyword.Bluemix_notm}} space that are trying to reach the host. If a port is specified in the Dockerfile for the image that you are using, include that port. <br><br><strong>Tips:</strong><ul><li>For the IBM certified Liberty Server image or a modified version of this image, enter port 9080.</li><li>For the IBM certified Node.js image or a modified version of this image, enter port 8000.</li></ul></dd>
   <dt>-P (optional)</dt>
   <dd>Automatically expose the ports that are specified in the image's Dockerfile for the HTTP traffic.</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (optional)</dt>
   <dd>Assign a memory limit to the group in MB. When you create a container group from the CLI, the default value for each container instance is 64 MB.  When you create a container group from the {{site.data.keyword.Bluemix_notm}} Dashboard, the default value for each instance is 256 MB. Accepted values are 64, 256, 512, 1024 and 2048. After a memory limit is assigned, the value can't be changed.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (optional)</dt>
   <dd>Set the environment variable, where <i>ENV</i> is a key=value pair. List multiple keys separately. If you include quotation marks, include them around both the environment variable name and the value. For example: -e "key1=value1" -e "key2=value2" -e "key3=value3". The following table shows some commonly used environment variables that you can specify:</dd>
   </dl>


|      Environment variable                          |   Description                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bind a service to a container. Use the `CCS_BIND_APP` environment variable to bind an app to the container. The app is bound to the target service and acts as a bridge that allows {{site.data.keyword.Bluemix_notm}} to bring your bridge app’s `VCAP_SERVICES` information into the running container instance. For more information about creating a bridge app, see [Binding a service to a container](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | To bind a Bluemix service directly to a container without using a bridge app, use CCS_BIND_SRV. This binding allows Bluemix to inject the VCAP_SERVICES information into the running container instance. To list multiple Bluemix services, include them as part of the same environment variable. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Add a log file to be monitored in the container. Include the `LOG_LOCATIONS` environment variable with a path to the log file. |
{: caption="Table 3. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (optional)</dt>
   <dd>Attach a volume to a container by specifying the details in the format <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: The volume ID or name.</li>
   <li><i>CONTAINER_PATH</i>: The absolute path to the volume in the container.</li>
   <li>ro: Optional. Specifying <i>ro</i> makes the volume read-only instead of the default read/write.</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (required)</dt>
   <dd>Assign a name to the container. <br> <strong>Tip:</strong> The container name must start with a letter. The name can include uppercase letters, lowercase letters, numbers, periods ., underscores _, or hyphens -.</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (optional)</dt>
   <dd>Whenever you want a container to communicate with another container that is running, you can address it by using an alias for the host name.</dd>
   <dt>-it (optional)</dt>
   <dd>Run the container in an interactive mode. After the container is created, keep the standard input displaying. Type <i>exit</i> to exit.</dd>
   <dt><i>IMAGE</i> (required)</dt>
   <dd>The image to be included in the container. You can list commands after the image, but don't put any options after the image. Include all options before specifying an image. Include all options before you specify an image. <br><br>If you use an image in your organization's private {{site.data.keyword.Bluemix_notm}} repository, specify the image in the format: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>If you use an image that is provided by IBM Containers, specify the image in the format: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>The command and arguments that are passed to the container group to execute. This command must be a long-running command. Do not use a short-lived command that does not run for very long, for example, <i>/bin/date</i>, because the short-lived command might cause the container to crash.</dd>
   </dl>


<strong>Examples</strong>:

Run the `sh -c "while true; do date; sleep 20; done"` long-running command on the `my_container` container that is built on the `registry.ng.bluemix.net/ibmnode` image.
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Create and then start a container `proxy` with a `1024` MB memory limit by using the `my_namespace/nginx` image, where `my_namespace` is the namespace associated with the logged-in users.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Create and then start a container by using the `my_namespace/blog` image, pass the credentials as environmental variables. `my_namespace` is the namespace associated with the logged-in users.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Add a volume to a container by using the `my_namespace/blog` image, where `my_namespace` is the namespace associated with the logged-in users.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

Add a service to a running container group. This command is available only to container groups. Single containers must bind a service as part of the bluemix ic run command.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Command options</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The group ID or name.</dd>
   <dt><i>SERVICE_INSTANCE</i> (required)</dt>
   <dd>The name of the service instance to be added to the container group.</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Remove a service from a running container group. This command is available only to container groups. Single containers must remove the container and create a new container without the service.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Command options</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The group ID or name.</dd>
   <dt><i>SERVICE_INSTANCE</i> (required)</dt>
   <dd>The name of the service instance to be added to the container group.</dd>
   </dl>


## bluemix ic start
{: #ic_start}
Start a stopped container. For more information, see the [start ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} command in the Docker help. To stop a container, see the [bluemix ic stop](#ic_stop) command.

```
bluemix ic start CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>


<strong>Responses</strong>:

- Started container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to start a container that is named `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

For one or more containers, view live usage statistics. Use `CTRL+C` to exit. For more information, see the [stats ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} command in the Docker help.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt>--no-stream (optional)</dt>
   <dd>Display only the latest result and do not include any information that precedes it.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request for the most recent statistics about a container:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic stop
{: #ic_stop}
Stop a running container. For more information, see the [stop ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} command in the Docker help. To start a container, see the [bluemix ic start](#ic_start) command.

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (optional)</dt>
   <dd>The number of seconds to wait before the container is killed.</dd>
   </dl>

<strong>Responses</strong>:

- Stopped container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to stop a container that is named `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

Show the processes that are running in the container. For more information, see the [top ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} command in the Docker help.

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to display the processes in a container that is called `my_container`.
```
bluemix ic top my_container
```


## bluemix ic unpause
{: #unpause}

Unpause all processes within a running container. For more information, see the [unpause ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} command in the Docker help. To pause a container, see the [bluemix ic pause](#pause) command.

```
bluemix ic unpause CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Responses</strong>:

- Unpaused container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to unpause a container that is named `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

Delete the IBM Containers service from the Bluemix space that you are logged into.

<strong>Attention</strong>: When you run this command, all your single containers and container groups are lost. Your space is still available in Bluemix. To start using the IBM Containers again, you must run `bluemix ic reprovision` to provision the IBM Containers service again.

```
bluemix ic reprovision [--force|-f]
```
<strong>Command options</strong>:

<dl>
   <dt>--force|-f (optional)</dt>
   <dd>Forces the deletion of the Bluemix from the Bluemix space.</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Show the version of Docker and the IBM Containers API.

```
bluemix ic version
```

<strong>Prerequisites</strong>:  Docker

To see the version of the IBM Containers, run `bluemix ic info`. For more information, see the [version ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} command in the Docker help.


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Create a volume.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>FS_NAME</i> (optional)</dt>
   <dd>The file share name. If no file share is available or named the volume will be built on the space's default file share.</dd>
   <dt><i>VOLUME_NAME</i> (required)</dt>
   <dd>The volume name. The name can contain lowercase letters, numbers, underscores _, and hyphens -.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to create a volume.
```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

List file shares.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Create a file share.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (required)</dt>
   <dd>The file share name. The name can contain lowercase letters, numbers, underscores _, and hyphens -.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to create a file share.
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

List all file share flavors.

```
bluemix ic volume-fs-flavors
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspect a file share.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (required)</dt>
   <dd>The file share name.</dd>
   </dl>

<strong>Examples</strong>:

The following example is a request to inspect a file share, where `my_file_share` is the name of the file share.
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Remove a file share.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (required)</dt>
   <dd>The file share name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to remove a file share, where `my_file_share` is the name of the file share.
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspect a volume.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (required)</dt>
   <dd>The volume name.</dd>
   </dl>

<strong>Examples</strong>:

The following example is a request to inspect a volume, where `volume_name` is the name of the volume.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Remove a volume.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (required)</dt>
   <dd>The volume name.</dd>
    </dl>

<strong>Examples</strong>:

The following example shows a request to remove a volume, where `volume_name` is the name of the volume.
```
bluemix ic volume-remove volume_name
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

List volumes.

```
bluemix ic volumes
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


## bluemix ic wait
{: #bluemix_ic_wait}

Exit a container and display the exit code as confirmation. For more information, see the [wait ![External link icon](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} command in the Docker help.

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to exit a container that is called `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

Wait for a single container or container group to reach a non-transient state. During this waiting time your command line does not return and you cannot enter commands. As soon as the container reaches a non-transient state, an OK message is displayed. For single containers, the non-transient states include Running, Shutdown, Crashed, Paused, or Suspended. For container groups, the non-transient states include CREATE_COMPLETE, UPDATE_COMPLETE, or FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to exit a container that is called `my_container`:
```
bluemix ic wait my_container
```
