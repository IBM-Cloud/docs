---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*Última atualização: 19 de março de 2016*

O tempo de execução do Tomcat no {{site.data.keyword.Bluemix}} foi desenvolvido com o java_buildpack.
{: shortdesc}

Para usar o tempo de execução do Tomcat no {{site.data.keyword.Bluemix}}, deve-se especificar o java_buildpack com a opção -b. Por exemplo:
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Para obter mais informações sobre o tempo de execução do Tomcat, veja o
[leia-me do java-buildpack](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do Tomcat.  O aplicativo iniciador do Tomcat é um app Tomcat simples que fornece um modelo que pode ser usado. É possível experimentar o app iniciador e fazer mudanças e enviá-las por push para o ambiente do Bluemix. Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

É possível mudar a versão do Tomcat a ser usada por seu app com a variável de ambiente JBP_CONFIG_TOMCAT.
É possível mudar a versão do Java a ser usada por seu app com a variável de ambiente JBP_CONFIG_OPEN_JDK_JRE.
Ambos podem ser especificados no arquivo manifest do aplicativo.  Por exemplo:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
A versão padrão atual do Tomcat é 8.0.30.  A versão padrão atual do Java é 1.8.0_65.
Para obter mais informações veja [Liberações do java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases).

# rellinks
## geral
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
