---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Comando de inicialização
{: #startup_commmand}

As maneiras recomendadas para especificar um comando inicial para seu aplicativo Bluemix Node.js são usar um arquivo **Procfile** ou um arquivo **package.json**.
{: shortdesc}

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

Para obter mais informações sobre o arquivo **Procfile** e **package.json**, veja [Dicas para aplicativos Node.js ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
