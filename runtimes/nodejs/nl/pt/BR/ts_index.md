---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolução de problemas do SDK for Nodejs
{: #ts}


Aqui estão as respostas para perguntas comuns de resolução de problemas sobre o uso do SDK for Nodejs no {{site.data.keyword.Bluemix}}.
{:shortdesc}

## O aplicativo falha ao ser iniciado com um erro "Não sobrou nenhum espaço no dispositivo"
{: #no_space_left_on_device}


Um aplicativo Nodejs falha ao ser iniciado com um erro "Não sobrou nenhum espaço no dispositivo". Por exemplo, o
erro nos logs pode ser semelhante ao seguinte:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Os aplicativos Nodejs que usam versões NPM anteriores à versão 3 consomem mais espaço ao fazer download de dependências.
{: tsCauses}

Modifique o arquivo package.json de seu aplicativo para usar uma versão NPM 3 ou superior.
{: tsResolve}

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
