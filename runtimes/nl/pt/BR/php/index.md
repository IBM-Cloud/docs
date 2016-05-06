---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*Última atualização: 16 de março de 2016*

O tempo de execução PHP no {{site.data.keyword.Bluemix}} foi desenvolvido com o php_buildpack.
O php_buildpack fornece um ambiente de tempo de execução completo para apps em PHP.
{: shortdesc}

O php_buildpack é usado nas condições a seguir:
* Seu app contém um arquivo composer.json ou
* seu app contém um arquivo *.php, ou
* seu app define uma variável ${WEBDIR} em seu arquivo
[options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) e essa variável está configurada para
um diretório existente dentro de seu app.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um app iniciador em PHP.  O aplicativo iniciador em PHP é um app em PHP simples que fornece um modelo
que pode ser usado para seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o
ambiente {site.data.keyword.Bluemix}}.  Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para
obter ajuda sobre o uso do app iniciador.

## Versões de tempo de execução
{: #runtime_versions}

É possível especificar a versão do PHP a ser usado por seu app no arquivo composer.json. Por exemplo:

```
{
    "versão": "1.5"
}
```
{: codeblock}
Para obter mais informações, consulte [Pacotes do Composer Platform](https://getcomposer.org/doc/02-libraries.md#platform-packages).

Quando uma versão não estiver especificada, a versão 5.5.30 será escolhida, por padrão.

### Versões disponíveis:
{: #available_versions}

As seguintes versões do PHP estão disponíveis no [buildback
PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5) atualmente instalado no {{site.data.keyword.Bluemix}}:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

Se seu app requer uma versão do PHP não listada, é possível usar o [buildpack
PHP](https://github.com/cloudfoundry/php-buildpack.git) externo para implementar o app.

# rellinks
## amostras
* [Compilar e implementar uma API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Compilar e implementar um contador de calorias fácil de usar em dispositivos móveis ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## geral
* [Buildpack do Cloud Foundry para PHP](https://github.com/cloudfoundry/php-buildpack.git)
