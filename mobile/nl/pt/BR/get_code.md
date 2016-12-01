---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obter código
{: #Get_Code}

Ao concluir a configuração e a instalação do seu projeto móvel
com os seus recursos selecionados, é possível fazer o download do
código que permite executar o código no Xcode ou no Android Studio. Seu projeto transferido por
download é pré-configurado com as dependências e credenciais do SDK necessárias para
cada recurso que você configurou.

Você precisará concluir as credenciais dos serviços que não são configuráveis em seu
projeto transferido por download. O arquivo `README.md` para o projeto
iniciador contém instruções. Visualize o arquivo `README.md` em um
visualizador de Redução de preço para concluir a configuração.

### Ferramentas do desenvolvedor de pré-requisito
{: #prereq-dev-tools}

As ferramentas do desenvolvedor a seguir são necessárias quando você está
trabalhando com código gerado a partir do painel do
{{site.data.keyword.Bluemix_notm}} Mobile:

#### Android
* [Android Studio 2.2](https://developer.android.com/studio)
	* Instale o tempo de execução mais recente do [Android 7.0](https://www.android.com/versions/nougat-7-0/).

#### iOS
* [Xcode
8.0](https://developer.apple.com/xcode/) (recomendado)
	* Instale o tempo de execução mais recente do [iOS 10](http://www.apple.com/ios/ios-10/).
* [Homebrew](http://brew.sh/)
	* Ferramenta de linha de comandos para ajudar na instalação de outras ferramentas
e tempos de execução, como CocoaPods e Carthage, para desenvolvedores da Apple.
* Gerenciador de dependência [CocoaPods](https://cocoapods.org/)
para instalar dependências do iOS SDK. Use a versão mais recente:

	```
	$ sudo gem install cocoapods --pre
	```
* Gerenciador de dependência
[Carthage](https://github.com/Carthage/Carthage) para instalar Watson Developer Cloud SDKs.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (tempos de execução do Node e NPM) para ajudar na execução do API
Connect Loopback e outras ferramentas de produtividade do Bluemix.

	Para executar as ferramentas de API Connect localmente, use o Node 5.x:
	```
	$ brew install Node5
	```

* [Ferramentas da CLI do Bluemix](http://clis.ng.bluemix.net/ui/home.html).
Ferramentas de linha de comandos para implementar facilmente os tempos de execução do
Cloud Foundry a partir de uma interface da linha de comandos com o Bluemix.  
