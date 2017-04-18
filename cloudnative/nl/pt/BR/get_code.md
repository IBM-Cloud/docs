---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obter código
{: #Get_Code}

Ao concluir a configuração e a instalação de seu projeto com os recursos selecionados, será possível fazer download do código que permitirá executá-lo. Seu projeto transferido por
download é pré-configurado com as dependências e credenciais do SDK necessárias para
cada recurso que você configurou.

Você precisará concluir as credenciais dos serviços que não são configuráveis em seu
projeto transferido por download. O arquivo `README.md` para o projeto
iniciador contém instruções. Visualize o arquivo `README.md` em um
visualizador de Redução de preço para concluir a configuração.

## Ferramentas do desenvolvedor de pré-requisito
{: #prereq-dev-tools}

As ferramentas do desenvolvedor a seguir são necessárias quando você está trabalhando com código gerado do {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}:


### Consultas
{: #general notoc}

* [Homebrew ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://brew.sh/)
	* Ferramenta de linha de comandos para ajudar na instalação de outras ferramentas
e tempos de execução, como CocoaPods e Carthage, para desenvolvedores da Apple.

* [Docker ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.docker.com/get-docker)
	* O projeto de software livre para ajudar na execução e depuração de aplicativos em contêineres. Necessário apenas para projetos não móveis.

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js (Tempos de execução do Node e npm) para ajudar na execução do {{site.data.keyword.apiconnect_short}} Loopback e outras ferramentas de produtividade do {{site.data.keyword.Bluemix_notm}}.

	Para executar as ferramentas do {{site.data.keyword.apiconnect_short}} localmente, use Node 5.x:
	
	```
	$ brew install Node5
	```

* [Ferramentas do Bluemix CLI ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://clis.ng.bluemix.net/ui/home.html)

   Ferramentas de linha de comandos para implementar tempos de execução do Cloud Foundry de uma interface da linha de comandos com o {{site.data.keyword.Bluemix_notm}}.  

* [{{site.data.keyword.dev_cli_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](dev_cli.html)

	Plug-in do {{site.data.keyword.Bluemix_notm}} CLI para criar, executar, testar e implementar projetos da web e móveis.
	
* [Plug-in do SDK Generator ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](sdk_cli.html)

	Plug-in do {{site.data.keyword.Bluemix_notm}} CLI para gerar SDKs de sua definição de API de REST compatível com a [Especificação de Open API ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.openapis.org/).

### Android
{: #android notoc}

* [Android Studio 2.2 ou superior![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://developer.android.com/studio)
	* Instale o tempo de execução mais recente do [Android 7.0 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.android.com/versions/nougat-7-0/).

### iOS
{: #ios notoc}

* [Xcode 8 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/xcode/) (recomendado)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* [Gerenciador de dependência do CocoaPods ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cocoapods.org/) para instalar dependências do SDK iOS. Use a versão mais recente:

	```
	$ sudo gem install cocoapods --pre
	```
* [Gerenciador de dependência do Carthage ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Carthage/Carthage) para instalar SDKs do {{site.data.keyword.watson}} Developer Cloud.

	```
	$ brew install carthage
	```
