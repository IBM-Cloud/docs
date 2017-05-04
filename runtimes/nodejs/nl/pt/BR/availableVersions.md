---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versões disponíveis
{: #available_versions}

{{site.data.keyword.Bluemix}} fornece todos os
[tempos de execução Node.js atualmente disponíveis](http://nodejs.org/dist/). Desses, a IBM fornece versões que contêm aprimoramentos e correções de bug. Consulte [Atualizações Mais Recentes para o Buildpack Node.js](/docs/runtimes/nodejs/updates.html) para obter mais informações.
{: shortdesc}

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
     "npm": "3.10.10"
  }
}
```
{: codeblock}

Uma versão do nó deve sempre ser especificada no arquivo **package.json**. Se não for, a versão do nó mais recente será usada.
