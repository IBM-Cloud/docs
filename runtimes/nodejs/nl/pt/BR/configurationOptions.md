---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Opções de configuração
{: #configuration_options}
{: shortdesc}

Há uma variedade de opções disponíveis para configurar o
buildpack sdk-for-nodejs.

## Scripts NPM
{: #npm_scripts}
NPM fornece um recurso de script permitindo que você execute scripts, incluindo os scripts **preinstall** e **postinstall**, que são aplicados antes e depois de seus node_modules serem instalados.  Veja [npm-scripts ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.npmjs.com/misc/scripts) para obter detalhes completos.

## Comportamento do cache
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
