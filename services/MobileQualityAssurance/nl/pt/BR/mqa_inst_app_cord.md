---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Instrumentando o MQA com um app Cordova (descontinuado)
{: #instrumentcord}

Para usar o {{site.data.keyword.mqafull}} com seu app Cordova, deve-se
fazer download do SDK e instrumentá-lo fazendo algumas mudanças usando a interface da
linha de comandos.
{: shortdesc}

Para poder instrumentar um app com o {{site.data.keyword.mqa}}, deve-se ter
uma conta do {{site.data.keyword.Bluemix}} e a versão corretamente instalada do
ambiente de desenvolvimento para as plataformas do app que você está instrumentando.

Para instrumentar o {{site.data.keyword.mqa}} para funcionar com seu app
Cordova, conclua as tarefas a seguir:

1. Inclua as permissões requeridas e o SDK transferido por download no seu projeto do Cordova.

	1. Abra um prompt de comandos e navegue para o diretório que contém seus arquivos de projeto.

	2. Inclua o plug-in do {{site.data.keyword.mqa}} em seu projeto do Cordova
concluindo as etapas a seguir, dependendo de seu ambiente:

		**Importante**: se você estiver usando Xcode 7.x no iOS 9,
deverá definir a configuração Ativar bitcode como Não nas Configurações de
construção do Xcode. É possível mudar essa configuração abrindo o Xcode usando o arquivo
do projeto do Cordova .xcodeproj, que está localizado na pasta platform\iPhone.

		* IBM MobileFirst™ Platform Foundation Versão 7.1:

			1. Insira o comando a seguir para instalar o plug-in do {{site.data.keyword.mqa}}:

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			Em que *plugin_location* é o caminho para o diretório do plug-in do {{site.data.keyword.mqa}} extraído que você transferiu por download.

			2. Se seu aplicativo for executado no Android, renomeie o arquivo
`project_name/app_name/platforms/android/custom_rules.xml` para
`custom_rules.xml.bak`.

		* Apache Cordova anterior à versão 4.0:
			1. Insira o comando a seguir para instalar o plug-in do
{{site.data.keyword.mqa}}:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Em que *plugin_location* é o caminho para o diretório do plug-in
do {{site.data.keyword.mqa}} extraído que você transferiu por download.

			2. Insira o comando a seguir para incluir um plug-in requerido adicional:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. Se seu aplicativo for executado no Android, renomeie o arquivo
`project_name/app_name/platforms/android/custom_rules.xml` para
`custom_rules_bak.xml`. 

		* Apache Cordova versão 4.0 ou mais recente:

			1. Insira o comando a seguir:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Em que *plugin_location* é o caminho para o diretório do plug-in
do Cordova do {{site.data.keyword.mqa}} extraído que você transferiu por download.

			2. Insira o comando a seguir para incluir um plug-in requerido adicional:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. Inicie uma nova sessão do {{site.data.keyword.mqa}} com cada log-in.

	1. Abra o arquivo `index.js` que está neste diretório: `your_project_name\www\js`.

	2. Inclua a função e os parâmetros a seguir dentro da função
`onDeviceReady()` que está no arquivo `index.js`. Coloque
a função antes da chave final da função.

	Restrição: Para um app já instrumentado para Mobile Quality
Assurance usando uma versão mais antiga do plug-in para Cordova para usar os recursos
incluídos no plug-in do Mobile Quality Assurance para Cordova versão 3.0.18 e mais
recente deve-se gerar novamente e substituir a chave do app. Para obter mais informações
sobre como gerar novamente a chave do app, consulte Gerenciando configurações de app. As
chaves de app que foram geradas antes de fevereiro de 2016 continuam funcionando com o
plug-in mais antigo, mas não funcionarão mais depois que você fizer upgrade do plug-in
para a versão 3.0.18 ou mais recente.

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. Continue com as etapas em [Introdução ao {{site.data.keyword.mqa}}](index.html).



# Links relacionados
{: #rellinks notoc}

## Links relacionados
{: #general notoc}
* [Introdução ao {{site.data.keyword.mqa}}](index.html){:new_window}
