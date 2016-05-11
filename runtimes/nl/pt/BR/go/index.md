---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Ir
{: #go_runtime}
*Última atualização: 16 de março de 2016*

O tempo de execução Go no {{site.data.keyword.Bluemix}} foi desenvolvido com o go_buildpack.
O go_buildpack fornece um ambiente de tempo de execução completo para apps Go.
{: shortdesc}

O go_buildpack é usado se seu aplicativo contém um arquivo chamado *.go.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do Go.  O aplicativo iniciador do Go é um app Go simples que fornece
um modelo que você pode usar para seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
Bluemix. Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para obter ajuda sobre o uso do
aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

É possível especificar a versão do Go a ser usada por seu app, configurando a propriedade GoVersion no arquivo
Godeps/Godeps.json na raiz de seu aplicativo. Por exemplo:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Para obter mais informações, veja [godep](https://github.com/tools/godep){: new_window}.

### Versões disponíveis:
{: #available_versions}

As seguintes versões do Go estão disponíveis no [buildpack Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2){: new_window}
atualmente instalado no {{site.data.keyword.Bluemix}}:

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1,5
* 1.5.1

Se o seu app requer uma versão do Go não listada,
é possível usar um [buildpack Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window} externo para implementar o aplicativo.

# rellinks
## geral
* [GoLang](http://golang.org/){: new_window}
* [Buildpack do Cloud Foundry para Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
