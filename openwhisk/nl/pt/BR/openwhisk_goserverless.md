---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Integração do OpenWhisk com Serverless Framework
{: #openwhisk_goserverless}

O [Serverless Framework](https://serverless.com/) é uma estrutura de software livre
para construir aplicativos sem servidor. Usando um arquivo manifest simples, os desenvolvedores podem
definir funções sem servidor, conectá-las a origens de eventos e declarar serviços em nuvem necessários pelo seu
aplicativo. A estrutura manipula a implementação desses aplicativos sem servidor nos provedores em nuvem.
Ela também permite que os desenvolvedores monitorem serviços em produção, atualizações de apresentação e
ajudem nos problemas de depuração. Ela também possui um ecossistema vibrante de plug-ins de terceiros para
estender a funcionalidade da estrutura. É aí que entra o OpenWhisk. {:shortdesc}

O OpenWhisk tem [seu próprio
plug-in de provedor para o Serverless Framework](https://github.com/serverless/serverless-openwhisk). Os desenvolvedores que usam o Serverless
Framework podem optar por implementar seus aplicativos em qualquer instância de plataforma do OpenWhisk
(hospedada no Bluemix, em outra nuvem ou privada). O suporte para múltiplos provedores
também significa que mover aplicativos entre plataformas é muito mais fácil e os desenvolvedores podem
desenvolver múltiplos aplicativos sem servidor na nuvem.

## Introdução
{: #openwhisk_goserverless_starting}

Aqui está o [Guia de
Introdução para o OpenWhisk](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/) oficial do Serverless Framework, que aborda a instalação, o fluxo de
trabalho de desenvolvimento, as melhores práticas, um guia passo a passo para construir e desenvolver um
aplicativo OpenWhisk funcional e muito mais.

[Este vídeo](https://youtu.be/GJY10W98Itc) explica como usar o Serverless Framework com o
plug-in do provedor OpenWhisk.
## Documentação
{: #openwhisk_goserverless_docs}

A documentação mais recente sobre como usar o OpenWhisk com o Serverless Framework
[pode ser localizada aqui](https://serverless.com/framework/docs/providers/openwhisk/).
## Amostras
{: #openwhisk_goserverless_samples}
[O repositório de exemplos GitHub do Serverless
Framework](https://github.com/serverless/examples) agora apresenta o OpenWhisk mostrando como construir APIs HTTP, planejadores baseados em
cron, funções de encadeamento e muito mais.
