---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}

O tempo de execução Node.js no {{site.data.keyword.Bluemix}} é desenvolvido com o buildpack sdk-for-nodejs.
O buildpack sdk-for-nodejs fornece um ambiente de tempo de execução completo para apps Node.js.
{: shortdesc}

O buildpack sdk-for-nodejs é usado quando o aplicativo contém um arquivo **package.json** no diretório-raiz.

## Aplicativo iniciador
{: #starter_application}

{{site.data.keyword.Bluemix}} fornece um aplicativo iniciador Node.js.  O aplicativo iniciador Node.js é um app Node.js simples que fornece um modelo que você pode usar para seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
Bluemix. Consulte [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para obter ajuda sobre o uso do
aplicativo iniciador.

## Comando de inicialização
{: #starup_commmand}

As maneiras recomendadas para especificar um comando inicial para seu aplicativo Bluemix Node.js são usar um arquivo **Procfile** ou um arquivo **package.json**.

Especifique um comando de startup em seu **Procfile** da forma a seguir. Aqui,
app.js é o script js de inicialização para seu aplicativo.
```
web: node app.js
```
{: codeblock}

Salve o
**Procfile** no diretório-raiz de seu aplicativo.

Se um **Procfile** não estiver presente, o buildpack IBM Bluemix Node.js verificará uma entrada scripts.start no arquivo **package.json**. Novamente,
no exemplo abaixo, app.js é o script js de inicialização para seu aplicativo.
```
{
    ...   
    "scripts": {
      "início": "node app.js"
    }
}
```
{: codeblock}

Se uma entrada do script de início estiver presente no **package.json**, um
**Procfile** será automaticamente gerado. O conteúdo do **Procfile** gerado automaticamente é:
```
    web: npm start
```
{: codeblock}

Para obter mais informações sobre o arquivo **Procfile** e **package.json**,
consulte [Dicas para aplicativos Node.js](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Sugestões para executar seu aplicativo Node.js localmente
{: #hints}

Use estas informações para facilitar a execução do seu aplicativo Node.js localmente e no Bluemix.

O exemplo a seguir mostra parte da origem para um arquivo **js**:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Com este código, quando o aplicativo está em execução no Bluemix, a variável de ambiente PORT contém o
valor da porta que é interno para o Bluemix e no qual o aplicativo atende as conexões recebidas. Quando o
aplicativo está sendo executado localmente, PORT não está definido, de modo que **3000** é
usado como o número da porta. Gravando dessa maneira, é possível executar o aplicativo localmente para fins de teste e no Bluemix sem fazer mudanças adicionais.

## Modo offline
{: #offline_mode}

Consulte [Modo off-line](offlineMode.html) para obter informações sobre como controlar o acesso do buildpack a sites externos. 

## App Management
{{site.data.keyword.Bluemix}} fornece vários utilitários para gerenciar e depurar seu app Node.js.  Consulte [Gerenciamento de App](/docs/manageapps/app_mng.html) para obter detalhes completos.

## Versões disponíveis
{: #available_versions}

{{site.data.keyword.Bluemix}} fornece todos os
[tempos de execução Node.js atualmente disponíveis](http://nodejs.org/dist/). Desses, a IBM fornece versões que contêm aprimoramentos e correções de bug. Consulte [Atualizações Mais Recentes para o Buildpack Node.js](/docs/runtimes/nodejs/updates.html) para obter mais informações.

O buildpack IBM Node.js armazena em cache as versões de tempo de execução da IBM. Portanto, se usar o tempo de execução do IBM SDK para Node.js em seu aplicativo, você obterá um desempenho mais rápido do aplicativo quando seu aplicativo for enviado por push para o Bluemix.

Use o parâmetro **node** na seção **engines** no arquivo **package.json** para especificar a versão do tempo de execução Node.js que você deseja executar.

Use o parâmetro **npm** na seção **engines** no arquivo **package.json** se precisar especificar uma versão de npm diferente da versão empacotada com o Node.js.  

Consulte o exemplo a seguir:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

Uma versão do nó deve sempre ser especificada no arquivo **package.json**. Se não for, a versão do nó mais recente será usada.

## Opções de configuração
{: #configuration_options}

### Scripts NPM
{: #npm_scripts}
NPM fornece um recurso de script permitindo que você execute scripts, incluindo os scripts **preinstall** e **postinstall**, que são aplicados antes e depois de seus node_modules serem instalados.  Consulte [npm-scripts](https://docs.npmjs.com/misc/scripts) para obter detalhes completos.

### Comportamento do cache
{: #cache_behavior}
{{site.data.keyword.Bluemix}} mantém um diretório de cache por aplicativo de nó, que é persistido entre as construções. O cache armazena dependências resolvidas para que elas não sejam transferidas por download e instaladas toda vez que o app for implementado.  Por exemplo, suponha que myapp dependa de **express**.  Em
seguida, na primeira vez que myapp for implementado, o módulo
**express** será transferido por download.  Em implementações subsequentes de myapp, a instância armazenada em cache de **express** será usada. O comportamento padrão é armazenar em cache todos os node_modules instalados pelo NPM e bower_components instalados pelo bower.

Use a variável NODE_MODULES_CACHE para determinar se o builpack Node usa ou ignora ou não o cache de construções anteriores. O valor padrão é true.  Para desativar o armazenamento em cache, configure NODE_MODULES_CACHE como false, por exemplo, por meio da linha de comandos cf:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Observe que os node_modules que estão incluídos em seu aplicativo não são armazenados em cache.

É possível usar uma matriz **cacheDirectories** em seu **package.json** de nível superior para alcançar um controle de baixa granularidade sobre quais módulos são armazenados em cache.  Quando o elemento **cacheDirectories** está presente em **package.json**, apenas os módulos que estão na matriz **cacheDirectories** serão armazenados em cache.  No exemplo a seguir, apenas node_modules e bower_components são armazenados em cache.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS MODE
{: #fips_mode}

O buildpack Nodejs versões v3.2-20160315-1257 e mais recentes suporta [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  Para
usar um mecanismo ativado para FIPS, configure a variável de ambiente FIPS_MODE como true.
Por exemplo:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

É importante entender que quando FIPS_MODE é true, alguns módulos de nó podem não
funcionar.  Por exemplo, **módulos de nó que usam
[MD5](https://en.wikipedia.org/wiki/MD5) falharão**, como
[Express](http://expressjs.com/).  Para Express, a configuração de
[etag](http://expressjs.com/en/api.html) como false no app Expess pode
ajudar a contornar isso. Por exemplo, é possível fazer o seguinte em seu código:
```
    app.set('etag', false);
```
{: codeblock}
Veja este [post de stackoverflow](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
para obter mais informações.

**NOTA**: o [Gerenciamento de
aplicativo](/docs/manageapps/app_mng.html) e o FIPS_MODE NÃO são suportados simultaneamente.  Se a variável de ambiente
BLUEMIX_APP_MGMT_ENABLE for configurada e a variável de ambiente FIPS_MODE for
configurada como true, o app falhará no estágio.

Há vários métodos de verificar o estado de FIPS_MODE:
<ul>
<li> É possível verificar o staging_task.log do aplicativo para obter uma mensagem
semelhante à seguinte:    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Essa mensagem indica que o mecanismo node.js ativado para FIPS está em execução, mas não necessariamente que o FIPS está em execução
</li>

<li> É possível verificar o valor de **process.versions.openssl**. Por exemplo:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Se a versão do SSL contiver "fips", a versão do SSL que está em uso suportará FIPS.  
</li>

<li> Para node.js versão 6 e acima, é possível verificar o valor retornado por crypto.fips em código conforme o seguinte:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Se o valor retornado for 1, o FIPS estará em uso. Observe que crypto.fips retornará
*undefined* para as versões do node.js anteriores a 6.
</li>
</ul>

#### Nodejs v4
{: #nodejs_v4_fips}

A tabela a seguir explica o comportamento do node.js v4 com FIPS:

|                 | Resultado        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS está em uso.
  * O staging_task.log incluirá a mensagem *Installing FIPS-enabled IBM SDK for Node.js*.
  * O valor retornado por process.versions.openssl conterá "fips".
* success (2)
  * FIPS *NÃO* está em uso.
  * O staging_task.log *NÃO* incluirá a mensagem *Installing FIPS-enabled IBM SDK for Node.js*.
  * O valor retornado por process.versions.openssl *NÃO* conterá "fips".

#### Nodejs v6
{: #nodejs_v6_fips}

Para executar no modo FIPS com o Node.js versão 6, além da configuração
**FIPS_MODE=true**, deve-se também incluir
**--enable-fips** no comando inicial conforme no exemplo a seguir:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

A tabela a seguir explica o comportamento do node.js v6 com FIPS.

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS está em uso.
  * O staging_task.log incluirá a mensagem *Installing FIPS-enabled IBM SDK for Node.js*.
  * O valor retornado por process.versions.openssl conterá "fips"
  * crypto.fips retornará 1, indicando que FIPS está em uso
* success (2)
  * FIPS *NÃO* está em uso.
  * O staging_task.log incluirá a mensagem *Installing FIPS-enabled IBM SDK for Node.js*.
  * O valor retornado por process.versions.openssl conterá "fips"
  * crypto.fips retornará 0, indicando que FIPS *NÃO* está em uso
* failure (3)
  * FIPS *NÃO* está em uso.
  * O staging_task.log *NÃO* incluirá a mensagem *Installing FIPS-enabled IBM SDK for Node.js*.
  * A preparação falhará com a mensagem "ERR node: bad option: --enable-fips"
* success (4)
  * FIPS *NÃO* está em uso.
  * O staging_task.log *NÃO* incluirá a mensagem *Installing FIPS-enabled IBM SDK for Node.js*.
  * O valor retornado por process.versions.openssl *NÃO* conterá "fips"
  * crypto.fips retornará 0, indicando que FIPS *NÃO* está em uso


## Buildpacks Node.js

O Bluemix fornece várias versões do buildpack Node.js.
* O buildpack **sdk-for-nodejs** criado pela IBM é o buildpack padrão usado para aplicativos Node.js no Bluemix.
* O **nodejs_buildpack** é um buildpack de comunidade fornecido pela comunidade do Cloud Foundry.

O buildpack **sdk-for-nodejs** tem precedência sobre o **nodejs_buildpack** no Bluemix. Se desejar usar o **nodejs_buildpack** com seu aplicativo em vez do buildpack **sdk-for-nodejs**, você deverá especificar seu buildpack, por exemplo, usando a opção -b com o comando **cf push**.

Geralmente, o buildpack **sdk-for-nodejs** atual e uma versão anterior estão disponíveis.  Para ver todos os buildpacks disponíveis, use o comando **cf buildpacks**.  Por exemplo:
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                      position          enabled          locked          filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# rellinks
{: #rellinks}
## geral
{: #general}
* [Atualizações mais recentes para o buildpack Node.js](/docs/runtimes/nodejs/updates.html)
* [App Management](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
