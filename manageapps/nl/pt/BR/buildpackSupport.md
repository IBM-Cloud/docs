---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Instrução de suporte ao buildpack
{: #buildpack_support_statement}

Última atualização: 8 de setembro de 2016
{: .last-updated}

## Buildpacks integrados da IBM
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET Core](../runtimes/dotnet/index.html)

A IBM suportará duas versões (n e n - 1) de cada buildpack de tempo de execução que fornece no Bluemix (por exemplo, IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21). Cada
buildpack irá fornecer e suportar uma ou mais versões principais de seu tempo de execução correspondente, conforme apropriado (por exemplo, IBM SDK, Java Technology Edition Versão 7 Liberação 1 e Versão 8). Os
buildpacks serão normalmente atualizados a cada duas semanas com a versão secundária mais recente do tempo de execução que estiver disponível. A política acima assegura que qualquer versão de tempo de
execução implementada será suportada por pelo menos 1 mês a partir do momento da implementação.

Problemas podem ser relatados com relação a qualquer versão do IBM Buildpack integrado suportada atualmente no Bluemix; no entanto, eles precisarão ser verificados com relação à versão mais
recente. Se um defeito for localizado, a IBM fornecerá uma correção em um nível futuro do tempo de execução e do buildpack correspondente. A IBM não fornecerá correções para versões principais e secundárias
anteriores (N-1, n-1). A IBM não fornecerá suporte para tempos de execução de comunidade mesmo ao usar buildpacks IBM, por exemplo, ao usar o Open JDK com o buildpack do Liberty. Esses tempos de execução de
comunidade seguem a mesma política de suporte que os "Buildpacks integrados da comunidade" abaixo.

## Buildpacks integrados da comunidade
{: #built-in_community_buildpacks}

Os Buildpacks integrados da comunidade a seguir são fornecidos pelo Cloud Foundry Community:

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

Atualizações para esses buildpacks serão feitas quando o Bluemix for atualizado para uma nova versão do Cloud Foundry. Problemas com esses tempos de execução no Bluemix podem ser relatados à IBM e vamos
ajudar a determinar se o Bluemix é a origem do problema. Para problemas relacionados ao Bluemix, a IBM fornecerá uma correção; no entanto, para defeitos no buildpack ou no próprio tempo de execução, a IBM
ajudará a relatá-los para a comunidade apropriada. A IBM não estará fornecendo correções para esses buildpacks e tempos de execução.

## Buildpacks externos
{: #external_buildpacks}


Para buildpacks externos, não será fornecido suporte pela IBM. Você pode precisar entrar em contato com a Cloud Foundry Community para obter suporte. 


