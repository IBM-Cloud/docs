---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Instrução de suporte ao buildpack
{: #buildpack_support_statement}


## Buildpacks integrados da IBM
{: #built-in_ibm_buildpacks}

Para o [Liberty for Java](/docs/runtimes/liberty/index.html), [SDK for Node.js](/docs/runtimes/nodejs/index.html) e [ASP.NET Core](/docs/runtimes/dotnet/index.html), a IBM dará suporte a duas versões (n & n - 1),
por exemplo, IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21. Cada buildpack fornecerá e suportará uma ou mais versões principais de seu tempo de execução correspondente, conforme apropriado, por
exemplo, IBM SDK, Java Technology Edition Versão 7 Liberação 1 e Versão 8. Os buildpacks serão atualizados normalmente uma vez por mês com a versão secundária mais recente do tempo de execução que está disponível.

Para o [IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html), a IBM fornecerá suporte para o buildpack correspondente à versão mais recente do Swift disponível em [Swift.org](http://swift.org). As atualizações para o buildpack estarão em sincronia com a versão liberada mais recente disponível do Swift.

Os problemas podem ser relatados com relação a qualquer versão do IBM Buildpack integrado suportada atualmente no {{site.data.keyword.Bluemix_notm}}, no entanto, eles precisarão ser verificados com relação à versão mais recente. Se um defeito for localizado, a IBM fornecerá uma correção em um nível futuro do tempo de execução e do buildpack correspondente. A IBM não fornecerá correções para versões principais e secundárias
anteriores (N-1, n-1). A IBM não fornecerá suporte para tempos de execução de comunidade mesmo ao usar buildpacks IBM, por exemplo, ao usar o Open JDK com o buildpack do Liberty. Esses tempos de execução de
comunidade seguem a mesma política de suporte que os "Buildpacks integrados da comunidade" abaixo.

## Buildpacks integrados da comunidade
{: #built-in_community_buildpacks}

Os Buildpacks integrados da comunidade a seguir são fornecidos pelo Cloud Foundry Community:

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

As atualizações para esses buildpacks serão feitas quando for feito upgrade do {{site.data.keyword.Bluemix_notm}} para uma nova versão do Cloud Foundry. Problemas com esses tempos de execução no {{site.data.keyword.Bluemix_notm}} podem ser relatados à IBM e ajudaremos a determinar se o
{{site.data.keyword.Bluemix_notm}} é a origem do problema. Para problemas relacionados ao {{site.data.keyword.Bluemix_notm}}, a IBM fornecerá uma correção, no entanto, para defeitos no buildpack ou no próprio tempo de execução, a IBM ajudará a relatá-los à comunidade apropriada. A IBM não estará fornecendo correções para esses buildpacks e tempos de execução.

## Buildpacks externos
{: #external_buildpacks}


Para buildpacks externos, não será fornecido suporte pela IBM. Você pode precisar entrar em contato com a Cloud Foundry Community para obter suporte.
