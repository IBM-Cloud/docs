---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}} 服务入门
{: #autoscaling}
上次更新时间：2016 年 11 月 2 日
{: .last-updated}

在 {{site.data.keyword.Bluemix_notm}} 中，您可以自动管理应用程序的容量。使用 {{site.data.keyword.autoscaling}} 服务，以自动提高或降低您的应用程序的计算能力。应用程序实例数会根据您定义的 {{site.data.keyword.autoscaling}} 策略自动调整。
{:shortdesc} 

## 目录
  * [使用 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.autoscaling}} 服务](#as-service)
  * [使用 {{site.data.keyword.autoscaling}} 服务配置 Node.js 应用程序](#node-asagent)
  * [通过 RESTful API 管理 {{site.data.keyword.autoscaling}} 服务](#RESTAPI)
  * [通过 {{site.data.keyword.autoscaling}} CLI 管理 {{site.data.keyword.autoscaling}} 服务](#CLI)
  * [{{site.data.keyword.autoscaling}} 服务的策略字段](#policy_fields)
  * [错误消息](#err_msg)

## 在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.autoscaling}} 服务
{: #as-service}

要使用 {{site.data.keyword.autoscaling}} 服务，请完成以下步骤：

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，单击*添加服务或 API*，然后从服务目录中的 DevOps 部分选择 {{site.data.keyword.autoscaling}} 服务。此时会打开新窗口，其中显示 {{site.data.keyword.autoscaling}} 服务的概述。
2. 选择要绑定 {{site.data.keyword.autoscaling}} 服务的应用程序，并单击*创建*。<br/>
*请记住：*只能将一个 {{site.data.keyword.autoscaling}} 服务绑定到一个应用程序。如果应用程序已经与其他 {{site.data.keyword.autoscaling}} 服务绑定，请不要在此步骤中选择该应用程序。否则，将遇到 CWSCV2004E 错误。<br/>这将显示“重新编译打包应用程序”窗口。
3. 在“重新编译打包应用程序”窗口中，单击*重新编译打包*，以在使用刚刚添加的新 {{site.data.keyword.autoscaling}} 服务之前重新编译打包应用程序。<br/><ul><li>对于 Liberty 应用程序，{{site.data.keyword.autoscaling}} 是自动配置的，并且已准备好在应用程序重新编译打包后使用。</li> <li>对于 Node.js 应用程序，您必须更新应用程序代码来启用 {{site.data.keyword.autoscaling}} 服务，才能将应用程序推送到 {{site.data.keyword.Bluemix_notm}}。请参阅[使用 {{site.data.keyword.autoscaling}} 服务配置 Node.js 应用程序](index.html#node_asagent)，以获取更多详细信息。</ul><br/>
重新编译打包应用程序完成后，可以开始为应用程序配置 {{site.data.keyword.autoscaling}} 服务。
4. 要为应用程序配置 {{site.data.keyword.autoscaling}}，请在 {{site.data.keyword.Bluemix_notm}} 用户界面中，单击绑定了 {{site.data.keyword.autoscaling}} 服务的应用程序。
5. 在仪表板的服务部分，单击 *Auto-Scaling* 图标。
6. 如果尚未执行此操作，请通过单击*创建 {{site.data.keyword.autoscaling}} 策略*为应用程序定义 {{site.data.keyword.autoscaling}} 策略。

现在，您可以为应用程序配置 {{site.data.keyword.autoscaling}} 策略、查看度量值统计信息或扩展历史记录。
<dl>
<dt>策略配置</dt>
<dd>使用此部分可创建或编辑扩展规则，以指定触发特定扩展活动的条件。<ul>
<li> 对于 Liberty for Java™ 应用程序，您可以定义堆、内存、响应时间和吞吐量的扩展规则。  
<li> 对于 Node.js 应用程序，您可以定义堆、内存和吞吐量的扩展规则。<li> 对于 Ruby 应用程序，您可以定义内存的扩展规则。</ul>
*注：*您可以为多个度量值类型定义多个扩展规则。不过，{{site.data.keyword.autoscaling}} 服务不会检测扩展策略之间是否有冲突。定义扩展策略时，您必须确保多个扩展规则之间不相互冲突。否则，因应用程序在这一分钟向内扩展，而在下一分钟向外扩展，您可能会看到实例总数变化不定。<br/><br/>
如果您的应用程序工作负载在高峰时间和空闲时间动态更改，那么可以创建扩展日程安排，以处理不同时间段内的不同扩展需求。使用日程安排中指定的“最小实例计数”参数来定义应用程序实例数的基线，同时动态扩展规则仍适用于触发向内扩展和向外扩展操作的日程安排。</dd>
<dt>度量值统计信息</dt>
<dd>显示应用程序各个实例的度量值统计信息。您可以查看平均统计信息，还可以选择特定实例来查看其统计信息。</dd>
<dt>扩展历史记录</dt>
<dd>显示应用程序的扩展历史记录。<ul>
<li> 过去一周：显示过去一周的扩展历史记录。
<li> 过去一个月：显示过去一个月的扩展历史记录。
<li> 定制范围：您可以设置时间段。</ul>
*注：*您可以通过选择“扩展状态”或“向内/向外扩展”来过滤历史记录。</dd>
</dl>


## 使用 {{site.data.keyword.autoscaling}} 服务配置 Node.js 应用程序
{: #node-asagent}

要在 Node.js 应用程序中启用 {{site.data.keyword.autoscaling}} 服务，除了服务供应和绑定步骤之外，还需要先完成以下步骤，然后再将应用程序推送到 {{site.data.keyword.Bluemix_notm}}。

1. 使用以下步骤更新 package.json 文件：<ol><li>为 `blumix-autoscaling-agent` 创建依赖关系条目，例如 `"bluemix-autoscaling-agent": "*"`。<br/><li>（可选）根据您为应用程序分配的内存，在 `scripts` 部分内设置堆限制，例如 `"start": "node --max-old-space-size=600 app.js"`。<br/>*注：*如果想要根据堆使用情况触发扩展，请为 `max-old-space-size` 设置值。如果启动应用程序时未设置该值，那么无论为应用程序分配的内存是多少，都将使用缺省 Node.js 堆限制 1.4GB，这可能会导致不正确的自动扩展决策。<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. 更新主要文件，以添加代理程序声明 `var as_agent = require('bluemix-autoscaling-agent');`。以下代码片段显示带有自动扩展代理程序声明的完整入口 js 文件。<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## 通过 RESTful API 管理 {{site.data.keyword.autoscaling}} 服务 
{: #RESTAPI}

{{site.data.keyword.autoscaling}} RESTful API 提供了 Bluemix UI 以外的另一种管理 {{site.data.keyword.autoscaling}} 服务的方法，并且还支持扩展数据检索和分析。与在 {{site.data.keyword.Bluemix_notm}} UI 中一样，API 提供类似功能，例如，创建策略和获取扩展历史记录。

要使用 {{site.data.keyword.autoscaling}} RESTful API 来管理 {{site.data.keyword.autoscaling}} 服务，请完成以下先决条件：按先前部分中指定将 {{site.data.keyword.autoscaling}} 服务与应用程序绑定，获取 `AccessToken`、{{site.data.keyword.autoscaling}} API 服务器的 URL 和要向内扩展或向外扩展的应用程序的 `app_id`：

1. 出于安全目的，在 {{site.data.keyword.autoscaling}} RESTful API 的每个请求头中，通过 CloudFoundry UAA 过程获取的正确 `AccessToken` 必须在 `Authorization` 头中提供，以指示请求所需的验证。不符合此 `AccessToken` 会导致“401 未授权”响应。安装 Cloud Foundry 命令行工具并登录到 {{site.data.keyword.Bluemix_notm}} 之后，有两种方法可以获取此 `AccessToken`：<ul><li>可以通过 `cf oauth-token` 命令获取此令牌：

   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
返回的以“bearer”开头的长字符串是 AccessToken，可用在 {{site.data.keyword.autoscaling}} RESTful API 的请求中。如果遇到“找不到命令”等错误，您可以将 Cloud Foundry 命令行工具更新到较新的版本。</li><li>您还可以在主目录中找到此 AccessToken。从命令行界面登录到 {{site.data.keyword.Bluemix_notm}} 之后，会在主文件夹中创建 `.cf` 文件夹，在其中您可以找到名为 `config.json` 的 JSON 文件，该文件包含当前日志记录的环境信息列表，例如，组织、空间、认证端点和版本。您可以在文件中找到如下所示的条目 `AccessToken`：
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
`config.json` 中的 `AccessToken` 仅在一段时间内有效。如果 REST API 请求得到“401 未授权”响应，那么您可能需要从命令行界面重新登录，以刷新文件并获取新的 `AcessToken`。</li></ul>
 
2.  在将应用程序与 {{site.data.keyword.autoscaling}} 服务绑定之后，可以通过检查 `VCAP_SERVICE` 环境变量来获取 {{site.data.keyword.autoscaling}} API 服务器的 URL。在 `VCAP_SERVICE` 中，您可以找到 {{site.data.keyword.autoscaling}} 服务部分，并且 `api_url` 是与应用程序绑定的 API 服务器的 URL。您需要此 API 服务器 URL 才能连接到 {{site.data.keyword.autoscaling}} RESTful API 服务：
   
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
请注意，还可通过 `cf env APPNAME` 命令找到此 URL：
   ```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   System-Provided:
   {"VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  可以从 `VCAP_SERVICES` 环境变量或只运行 `cf app APPNAME --guid` 命令来获取 `app_id`：

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

具备上述所有先决条件后，您现在可以在浏览器中使用 RestClient 附加组件或只通过某些工具（如 `curl`）提出 REST API 请求。 

使用 REST 客户机附加组件（如 Firefox 或 Chrome 的那些附加组件），可以对 {{site.data.keyword.autoscaling}} API 服务器触发执行命令的 REST 请求。您只要向这些附加组件提供 REST API 的 URL、此 REST API 所需的方法和头，以及主体部分中的参数。有关每个 API 的更多详细信息，请参阅 [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} 的 Rest API](https://new-console.ng.bluemix.net/apidocs/48){:new_window}。

使用 `curl` 等工具，可以管理脚本中的 {{site.data.keyword.autoscaling}} 服务，如下所示：    
```
cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## 通过 {{site.data.keyword.autoscaling}} CLI 管理 {{site.data.keyword.autoscaling}} 服务 
{: #CLI}

{{site.data.keyword.autoscaling}} CLI 提供的功能与 {{site.data.keyword.autoscaling}} RESTful API 提供的功能类似，但是配置 {{site.data.keyword.autoscaling}} 服务的方式更友好。使用 {{site.data.keyword.autoscaling}} CLI，您不需要关心 {{site.data.keyword.autoscaling}} RESTful API 中的详细信息（例如，`AccessToken` 和 API 服务器的 URL）。您只需要按照 CLI 提供的分步骤指示信息进行操作即可。有关如何安装和使用 {{site.data.keyword.autoscaling}} CLI 的更多详细信息，请参阅 [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}



## {{site.data.keyword.autoscaling}} 服务的策略字段
{: #policy_fields}

| 字段名称  | 描述 |
|-------------|----------------------|
|*允许的最大实例计数* |	可以启动的最大应用程序实例数。如果应用程序实例当前的数量等于此值，{{site.data.keyword.autoscaling}} 服务不再向外扩展应用程序。缺省最小实例计数是指可以启动的最小应用程序实例数。如果实例的数量等于此值，{{site.data.keyword.autoscaling}} 服务不再向内扩展应用程序。 |
| *度量值类型*	| 	可监视的受支持度量值类型。有关更多信息，请参阅“表 2”。 |
| *向外扩展* | 	指定触发向外扩展操作的阈值，以及触发向外扩展操作时要增加的实例数。 |
| *向内扩展* |	指定触发向内扩展操作的阈值，以及触发向内扩展操作时要减少的实例数。 |
| *统计信息窗口* |	过去一段时间长度，在此期间，收到的度量值被识别为有效。仅当时间戳记在此期间内时，度量值才有效。“统计信息窗口”参数的单位是秒。 |
| *违规持续时间*	| 过去一段时间长度，在此期间，可能会触发扩展操作。当所收集的度量值超过阈值上限或低于阈值下限（超过指定的时间）时，会触发扩展操作。“违规持续时间”参数的单位是秒。 |
| *向内扩展冷却期* | 发生向内扩展操作后，会在“向内扩展冷却期”参数所指定的时间长度内忽略其他扩展请求。此参数的单位是秒。 |
| *向外扩展冷却期*	| 发生向外扩展操作后，会在“向外扩展冷却期”参数所指定的时间长度内忽略其他扩展请求。此参数的单位是秒。 |
| *时区*	| 日程安排应用的时区。 |
| *开始时间*  |	重现日程安排的开始时间。 |
| *结束时间*    |	重现日程安排的结束时间。	|
| *重复日期*	|	重现日程安排应用时的日期。 |
| *最小实例计数* |	日程安排中指定时间段内可以对应用程序启动的最小实例数。 |
| *开始日期和时间* |	日程安排的开始日期和时间设置为特定日期。 |
| *结束日期和时间* |	日程安排的结束日期和时间设置为特定日期。	|

表 1. 扩展策略中的策略字段

| 度量值名称 | 描述 | 支持的应用程序类型 |
|-------------|----------------------| ------------------- |
| *堆* |	堆内存的使用百分比。	| Liberty for Java、Node.js SDK |
| *内存*   |	内存的使用百分比。	|  全部 |
| *吞吐量* | 每秒处理的请求数。| Liberty for Java、Node.js SDK |
| *响应时间* |	已处理的请求的响应时间。	| Liberty for Java |

表 2. 支持的度量值名称

*注：*要收集自动缩放度量数据，必须将应用程序部署为 Liberty Web 应用程序，这样才能通过 Liberty Web 容器处理度量 HTTP/HTTPS 请求。例如，如果将 Spring Boot 应用程序作为“Main-Class”应用程序运行，那么 Liberty buildpack 会只为您提供 java 环境，而应用程序实际在 Spring 嵌入式 Tomcat 容器中运行，因此自动缩放服务不会收集任何度量数据。必须将应用程序作为 Liberty WAR 运行，这样才能使用自动缩放服务。

## 错误消息
{: #err_msg}
本部分列出了 {{site.data.keyword.autoscaling}} 服务生成的警告和错误消息。
 
### CWSCV2004E 其他 {{site.data.keyword.autoscaling}} 服务已经绑定到该应用程序。
**只能将一个 {{site.data.keyword.autoscaling}} 服务绑定到一个应用程序。要将 {{site.data.keyword.autoscaling}} 服务绑定到已经与其他 {{site.data.keyword.autoscaling}} 服务绑定的应用程序时，会发生此错误。**

请选择没有与其他任何 {{site.data.keyword.autoscaling}} 服务绑定的其他应用程序，然后将目标 {{site.data.keyword.autoscaling}} 服务绑定到此应用程序。如果在其他所有情况下都遇到此错误，请联系 IBM 支持人员。

### CWSCV6001E API 服务器无法解析 API 的输入 JSON 字符串：{0}。
**解析输入 JSON 字符串时发生问题。**

请对照 API 文档检查输入 JSON，并更正其中的错误。

### CWSCV6002E API 服务器无法解析 API 的输出 JSON 字符串：{0}。
**解析输入 JSON 字符串时发生问题。**

请联系云管理员，以获取更多信息。

### CWSCV6003E API 的输入 JSON {1} 中的输入 JSON 字符串格式错误：{0}。
**解析输入 JSON 字符串时发现格式错误。**

请对照 API 文档检查输入 JSON，并更正其中的错误。

### CWSCV6004E API 的输出 JSON {1} 中的输出 JSON 字符串格式错误：{0}。
**解析输出 JSON 字符串时发现格式错误。**

请联系云管理员，以获取更多信息。

### CWSCV6005E {0} 期间发生内部服务器错误。
**处理请求时发生内部服务器错误。**

请联系云管理员，以获取更多信息。

### CWSCV6006E 调用 CloudFoundry API 失败：{0}
**调用 CloudFoundry API 时发生错误。**

请联系云管理员，以获取更多信息。

### CWSCV6007E 未找到应用程序：{0}
**未找到应用程序。**

请检查应用程序信息，以获取更多信息。

### CWSCV6008E 检索应用程序 {0} 的信息时发生以下错误：{1} 
**检索应用程序信息失败，并伴随一些错误。**

请检查应用程序信息，以获取更多信息。

### CWSCV6009E 未找到应用程序 {1} 的服务 {0}。
**找不到此应用程序的服务。**

请检查此应用程序的服务绑定，以获取更多信息。

### CWSCV6010E 找不到应用程序 {0} 的策略
**找不到此应用程序的策略。**

请检查应用程序配置，以获取更多信息。

### CWSCV6011E {0} 期间内部认证失败
**内部认证失败。**

请联系云管理员，以获取更多信息。


# 相关链接
{: #rellinks}

## 样本
{: #samples}

* [Tutorial: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Lab](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [Rest API of IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://new-console.{DomainName}/apidocs/48){:new_window}

## 常规
{: #general}

* [扩展容器](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [扩展虚拟服务器](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [适用于 Node.js 的 {{site.data.keyword.autoscaling}} 代理程序](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

