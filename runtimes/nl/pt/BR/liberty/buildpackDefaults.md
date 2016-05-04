---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Padrões de buildpack
{: #buildpack_defauts}

*Última atualização: 23 de março de 2016*

O buildpack do Liberty é atualizado frequentemente no Bluemix. Cada liberação pode conter correções de segurança ou aprimoramentos de recurso.

O buildpack possui valores padrão para configurações como
a versão Java ou o recurso Liberty configurados para os aplicativos WAR ou EAR. Alguns dos valores padrão podem mudar entre a liberação do buildpack,
o que pode impactar de modo adverso o aplicativo. Para evitar que o aplicativo
seja afetado pela mudança em padrões de buildpack, execute as etapas
para configurar o aplicativo e evitar o uso dos padrões de buildpack.

## Recursos do Liberty
{: #liberty_features}

Quando
você implementar os arquivos WAR ou EAR, o buildpack fornecerá uma configuração
para o aplicativo com um conjunto padrão de recursos do Liberty. Embora
raro, esse conjunto padrão de recursos do Liberty pode mudar entre as
liberações de buildpack. A mudança no conjunto de recursos padrão pode afetar de modo
adverso o aplicativo. Existem opções para assegurar que o aplicativo
não seja afetado pela mudança nos padrões de recursos.

* Configure a variável de ambiente JBP_CONFIG_LIBERTY para especificar explicitamente
uma lista de recursos ativados para o aplicativo. Para obter mais informações, veja [Aplicativos independentes](optionsForPushing.html#stand_alone_apps).
* Implemente seu aplicativo como um [diretório do
servidor](optionsForPushing.html#server_directory) ou um [servidor
em pacote](optionsForPushing.html#packaged_server). Forneça um arquivo server.xml customizado que especifique o conjunto exato dos recursos necessários para seu aplicativo.

Os aplicativos que são implementados como um diretório do servidor ou
um servidor em pacote não são afetados pela mudança no padrão de recursos do
Liberty.

## versão Java
{: #java_version}

O buildpack
fornece um JRE padrão para o aplicativo. A versão principal ou secundária
do JRE pode mudar entre as liberações de buildpack. A versão
secundária do JRE pode ser atualizada frequentemente enquanto a versão principal
é raramente atualizada. A mudança na versão principal do JRE pode
afetar de modo adverso o aplicativo.

Para assegurar que o aplicativo não seja afetado pela mudança da versão principal, configure a variável de ambiente com a versão apropriada do JRE, conforme descrito em [Customizando o JRE](customizingJRE.html). Para obter os melhores resultados,
adote o Java 8 para seus aplicativos.

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
