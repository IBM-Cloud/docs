---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Trabalhando com um proxy
{: #working_with_proxy}



Em alguns ambientes como [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) e
[Bluemix Local](/docs/local/index.html#local), um proxy
pode ser configurado que afeta o comportamento de seu aplicativo durante preparação e
tempo de execução.

É possível configurar seu aplicativo para trabalhar com o proxy usando as variáveis
de ambiente a seguir:
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

É possível configurar essas variáveis de ambiente usando *cf si* ou
por meio do arquivo *manifest.yml*.  Se seu aplicativo requerer que os
recursos sejam transferidos por download pela Internet durante a preparação e uma variável
de ambiente de proxy estiver configurada, dependendo de como as variáveis de ambiente de
proxy estiverem configuradas, seus recursos serão transferidos por download por meio do proxy
configurado.

Por exemplo, suponha que você tenha um aplicativo nodejs e ele esteja em execução em
um ambiente com *http_proxy* configurado como *yourProxyURL*.  Além
disso, suponha que você deseja permitir que o npm faça download de módulos de
nó pela Internet. Para fazer isso, você poderia configurar *no_proxy* como
*npmjs.org*.

**Nota**: Pode ser o caso de seu aplicativo aproveitar a
vantagem do proxy durante o tempo de execução.  Isso dependente inteiramente do
aplicativo e não é afetado pelo buildpack e qualquer uma dessas três variáveis de
ambiente.

## aplicativos Java
{: #java_apps}

Para [Liberty for Java](/docs/runtimes/liberty/index.html) e os aplicativos [java_buildpack](/docs/runtimes/tomcat/index.html), as configurações de proxy podem ser passadas ao tempo de execução por meio da variável de ambiente **JAVA_OPTS**.  Por exemplo, é possível emitir o comando:
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

e remontar seu aplicativo.  Seu aplicativo então usará as configurações de proxy
especificadas no tempo de execução. Consulte
[Redes
e proxies Java](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html) para obter mais informações sobre as opções de proxy Java.

# rellinks
{: #rellinks notoc}
## gerais
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
