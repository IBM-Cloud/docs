---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

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
* [Android Studio 2.2 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://developer.android.com/studio "Ícone de link externo")
	* Instale o tempo de execução mais recente do [Android 7.0 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.android.com/versions/nougat-7-0/ "Ícone de link externo").

#### iOS
* [Xcode 8.0 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://developer.apple.com/xcode/ "Ícone de link externo") (recomendado)
	* Instale o tempo de execução mais recente do [iOS 10 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www.apple.com/ios/ios-10/ "Ícone de link externo").
* [Homebrew ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://brew.sh/ "Ícone de link externo")
	* Ferramenta de linha de comandos para ajudar na instalação de outras ferramentas
e tempos de execução, como CocoaPods e Carthage, para desenvolvedores da Apple.
* Gerenciador de dependência do [CocoaPods ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cocoapods.org/ "Ícone de link externo") para instalar dependências do SDK iOS. Use a versão mais recente:

	```
	$ sudo gem install cocoapods --pre
	```
* Gerenciador de dependência do [Carthage ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Carthage/Carthage "Ícone de link externo") para instalar SDKs do Watson Developer Cloud.

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

* [Ferramentas de CLI do Bluemix ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://clis.ng.bluemix.net/ui/home.html "Ícone de link externo").
Ferramentas de linha de comandos para implementar facilmente os tempos de execução do
Cloud Foundry a partir de uma interface da linha de comandos com o Bluemix.  
