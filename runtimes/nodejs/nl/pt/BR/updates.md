---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Atualizações mais recentes para o buildpack do SDK for Nodejs
{: #latest_updates}

Uma lista das atualizações mais recentes no buildpack sdk-for-nodejs.

## 10 de março de 2017: atualizado o buildpack do Node.js v3.11
Essa liberação do buildpack suporta as versões de runtime do IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.3, 4.8.0, 6.9.5 e 6.10.0. A versão padrão agora é 4.8.0.

Além dos novos tempos de execução, essa liberação contém uma correção para um erro encontrado ao ativar o manipulador de gerenciamento de app shell usando a UI do devconsole. Esse buildpack também muda o modo de funcionamento da configuração automática do serviço Monitoring and Analytics. Os aplicativos que usam o plano Gratuito não terão mais a capacidade de log incluída em seus aplicativos, ele está sendo substituído por logmet.

## 20 de janeiro de 2017: atualizado o buildpack do Node.js v3.10
Essa liberação do buildpack suporta as versões de runtime do IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.0, 4.7.2, 6.9.2 e 6.9.4. O padrão agora é 4.7.2.

Ela contém uma correção para um erro em que "npm start" nem sempre foi chamado para iniciar aplicativos.

## 17 de novembro de 2016: atualizado o buildpack do Node.js v3.9
Essa liberação do buildpack suporta as versões de runtime do IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.16, 0.12.17, 4.6.1, 4.6.2, 6.7.0 e 6.9.1. O padrão agora é 4.6.2.

Observe que o Node.js v6 foi promovido para o status LTS em 18 de outubro de 2016 e em breve se tornará o tempo de execução padrão do buildpack. Node.js v0.10 atingiu o término de vida em 31 de outubro de 2016 e em breve não será mais incluído no buildpack. Veja [Suporte de longo prazo da versão do Node.js e o buildpack do SDK for Node.js](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) para obter mais detalhes.

Os erros que afetam os manipuladores de rastreio e inspetor do App Management, quando usados em conjunto com o Node.js v6, foram tratados nessa liberação. Veja [Gerenciando apps Liberty e Node.js](/docs/manageapps/app_mng.html#inspector) para obter mais informações sobre como o manipulador do inspetor está mudando, agora que o Node.js v6 integrou o recurso de inspetor.

## 7 de outubro de 2016: atualizado o buildpack do Node.js v3.8-20161006-1211
Esta liberação do buildpack suporta as versões de runtime do IBM SDK for Node.js: 0.10.46, 0.10.47, 0.12.15,
0.12.16, 4.5.0, 4.6.0, 6.6.0 e 6.7.0. O padrão agora é 4.6.0.

Além dos novos tempos de execução, esta liberação contém correções de erro do buildpack. Uma correção para o problema conhecido ao usar o Node.js 6.x e o Modo de desenvolvimento que foi mencionado
nas atualizações de liberação v3.7-20160826-1101 é uma delas. Ela também é sincronizada com o
[Buildpack do Cloud Foundry Node.js
v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20).

## 26 de agosto de 2016: atualizado o buildpack do Node.js v3.7-20160826-1101
Esta liberação do buildpack suporta as versões de runtime do IBM SDK for Node.js: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.7, 4.5.0, 6.2.2 e 6.4.0. O padrão agora é 4.5.0.

Esta liberação inclui correções de erro, inclusive aquelas do
[buildpack
1.5.18 do Node.js do Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18).

A liberação remove o suporte do manipulador de gerenciamento de app strongpm conforme anunciado em
[Bluemix
Node.js Buildpack v3.3 – modo FIPS e mais](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/).

Observe que há um problema conhecido ao usar o Node.js 6.x e o
[Modo de desenvolvimento](/docs/manageapps/app_mng.html#devmode). Como
solução alternativa, será necessário remontar seu aplicativo depois de ativar o modo de
desenvolvimento para poder começar a utilizá-lo.

## 22 de julho de 2016: atualizado o buildpack do Node.js v3.6-20160715-0749
Esta liberação do buildpack suporta as versões de runtime do IBM SDK for Node.js: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.6, 4.4.7, 6.2.1 e 6.2.2. O padrão agora é 4.4.7.

Esta liberação inclui um proxy de Gerenciamento de app atualizado que suporta logins federados.

Estão incluídas correções para as vulnerabilidades de segurança a seguir:
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 22 de junho de 2016: atualizado o buildpack do Node.js v3.5-20160609-1608

Esta liberação do buildpack inclui as versões de runtime 4.4.5 e 6.2.0 do IBM SDK for Node.js. O valor se torna 4.4.5.

A liberação remove o suporte para versões de runtime mais antigas, conforme anunciado em
[Bluemix
Node.js Buildpack v3.3 – modo FIPS e muito mais](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/). O buildpack agora suporta
0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0 e 6.2.0.

Esta liberação inclui correções de erro do [buildpack 1.5.14 do Node.js do Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14).

## 20 de maio de 2016: atualizado o buildpack do Node.js v3.4-20160518-1653

Esta liberação do buildpack inclui as versões de runtime 0.10.45, 0.12.14, 4.4.4, 6.0.0 e 6.1.0 do IBM SDK for Node.js. O padrão agora é 4.4.4.

Estão incluídas correções para as vulnerabilidades de segurança a seguir:
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.openssl.org/news/secadv/20160503.txt)

Observe que há um problema conhecido com o npm v3 e o utilitário inspetor de
Gerenciamento de app. O npm 3.8.6 é o padrão com os tempos de execução 6.0.0 e 6.1.0. Se
você quiser usar qualquer um dos tempos de execução 6.x e o utilitário inspetor, será necessário
especificar uma versão 2.x npm no package.json como solução alternativa provisória.

## 29 de abril de 2016: atualizado o buildpack do Node.js v3.3-20160428-1409

Esta liberação do buildpack inclui as versões de runtime 0.10.44, 0.12.13, 4.4.0,
4.4.1, 4.4.2 e 4.4.3 do IBM SDK for Node.js. O padrão agora é 4.4.3.
i
Para 4.3.1 e acima, agora é possível usar uma versão ativada para FIPS do tempo de
execução configurando a variável de ambiente `FIPS_MODE=true` para o app.

O buildpack atualizado e as novas versões de runtime também contêm correções para vulnerabilidades de segurança:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

O buildpack atualizado contém também correções para diversos erros:
* Agora as construções do IBM SDK for Node.js serão sempre usadas se houver uma disponível correspondente ao intervalo solicitado. Anteriormente, esse caso era verdadeiro somente para versões de runtime 4.x.
* Agora o utilitário inspetor do App Management funcionará com as versões de runtime 4.x.
* Corrigida uma regressão no utilitário strongpm do App Management.

## 18 de março de 2016: atualizado o buildpack do Node.js v3.2-20160315-1257

Esta liberação do buildpack move o tempo de execução do IBM SDK for Node.js padrão da versão 4.3.0 para 4.3.2. Também inclui o IBM SDK for Node.js versões 0.10.43, 0.12.12 e 4.3.1. Use essas versões recentes do Node.js para selecionar correções de diversas vulnerabilidades de segurança.

## 4 de março de 2016: atualizado o buildpack do Node.js v3.1-20160222-1123

Esta liberação do buildpack move o tempo de execução do IBM SDK for Node.js padrão da versão 4.2.4 para 4.3.0. Também inclui o IBM SDK for Node.js versões 0.10.42, 0.12.10 e 4.2.6. Use essas versões recentes do Node.js para selecionar correções de diversas vulnerabilidades de segurança.

## 4 de fevereiro de 2016: atualizado o buildpack do Node.js v3.0-20160125-1224

Esta liberação é totalmente sincronizada com o buildpack do [Node.js da comunidade do Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Além
das mudanças da comunidade, foram feitas modificações em determinados padrões, com
otimizações para reduzir o tempo de preparação e as atualizações para o recurso de
Gerenciamento de app.

* Atualizações do buildpack:

  * O Node.js v4.2.4 (IBM SDK for Node.js Versão 4) agora é o tempo de execução padrão no Bluemix, substituindo o v0.12.9. Essa mudança poderá fazer com que seu aplicativo se comporte de maneira diferente se uma
determinada versão não for especificada para ele. Para saber como especificar uma versão do Node.js para seu aplicativo Bluemix, veja a documentação [Tempo de execução do Node.js](index.html).

  * NODE_ENV está agora configurado como *production* por padrão. Essa mudança fará com que algumas dependências de nó se comportem de maneira diferente. Por exemplo, a estrutura Express não retornará mais rastreios de pilha no navegador da web para terminais com falha; em vez disso, exibirá *Erro interno do servidor*. Quando NPM_CONFIG_PRODUCTION for configurado como *true*, o NPM configurará NODE_ENV como *production* para scripts subshell somente na fase de instalação do npm. Essa
função permite que os usuários configurem NODE_ENV para outro valor como
*development* para o tempo de execução do aplicativo. Para clareza, os scripts npm verão a mensagem **NODE_ENV=production**.

  * Uma correção de bug para o serviço Monitoring and Analytics está incluída.

* Atualizações de armazenamento em cache:

  * Se o cache estiver desativado (NODE_MODULES_CACHE=false), o buildpack não tentará armazenar em cache nenhum módulo/componente. Anteriormente, essa configuração fazia isso para que o cache não estourasse, mas ainda armazenava em cache os módulos instalados para implementações futuras. Agora, ela não estourará o cache nem tentará armazenar qualquer cache.

  * Bower_components são armazenados em cache por padrão, além de node_modules.

* Outras atualizações:

  * Incluídos avisos úteis para dependências ausentes como gulp, bower e angular.

  * O script de detecção é atualizado com as informações da versão do buildpack.

  * A recomendação de armazenamento em cluster (WEB_CONCURRENCY) introduzida inicialmente pela comunidade foi removida porque a determinação de memória era inexata no Bluemix.


## 16 de dezembro de 2015: atualizado o buildpack do Node.js v2.8-20151209-1403 e v3.0beta-20151211-2041

Esta liberação do buildpack Node.js é fornecida com duas versões, v2.8 e v3.0beta. Ambas as versões incluem as mudanças a seguir:

Uma Correção de bug para o serviço de Monitoramento e Analítica
A inclusão de um tempo de execução armazenado em cache para o IBM SDK for Node.js
v4.2.3.0, v4.2.2.0, v1.2.0.8 e v1.2.0.7, com base nas versões da comunidade Node.js
v4.2.3, v4.2.2, v0.12.9 e v0.12.8.
Além disso, no v3.0beta, o tempo de execução do Node.js padrão mudou para v4.2.3.

O IBM Node.js buildpack v3.0beta agora é liberado como um buildpack não padrão no
Bluemix com Node.js v4.2.3 como tempo de execução padrão. Para assegurar que seus apps e
serviços continuarão funcionando no Bluemix, envie por push seu aplicativo com a versão
beta do buildpack. Após 30 dias ou mais, v3 se tornará o buildpack padrão.

Para enviar por push seu aplicativo com v3.0beta:
* Use a opção "-b" em seu comando 'cf push':

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Ou use a opção "buildpack" no arquivo manifest.yml:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Essa mudança no tempo de execução padrão não afetará seu aplicativo se você tiver
configurado uma versão específica do Node.js no package.json de seu aplicativo.

**Nota:**
sempre é possível especificar a versão do Node.js para executar seu aplicativo usando a
entrada engines.node em seu package.json conforme explicado em
[Versões disponíveis](index.html#available_versions).

## 23 de novembro de 2015: atualizado o buildpack do Node.js v2.7-20151118-1003

Com a 2.7, a versão 4.2.1.0 do IBM SDK for Node.js (com base em Node v4.2.1 LTS)
foi incluída. Ele ainda não é o padrão, mas pode ser especificado para uso. **Nota:**
essa versão substitui a construção de software livre que estava disponível anteriormente. Também
fizemos algumas pequenas correções de bug para nossa estrutura de extensão de serviço.

## 19 de outubro de 2015: atualizado o buildpack do Node.js v2.6.1-20151015-1326

O Node.js v2.6.1 apresenta uma correção de bug para o [Manipulador de gerenciamento do app StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) e uma versão mais consistente de NPM.

## 15 de outubro de 2015: atualizado o buildpack do Node.js v2.6-20151006-1309

Essa liberação do buildpack do Node.js apresenta a integração do [Gerenciador de processos StrongLoop ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://strong-pm.io) para o recurso App Management. Para obter mais informações, consulte a postagem do blog [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 de junho de 2015: atualizado o buildpack do Node.js v2.0-20150608-1503

Nesta liberação, nós sincronizamos nosso buildpack do Node.js com o mais recente
[Buildpack do Node.js da
comunidade CF](https://github.com/cloudfoundry/nodejs-buildpack), que é fornecido com inúmeros novos recursos da comunidade.
Além disso, reforçamos o recurso Gerenciamento de app no buildpack do Node.js, que
permite utilitários como shell, node-inspector, Bluemix Live Sync e muito mais. Consulte [Gerenciamento de App](/docs/manageapps/app_mng.html) para obter detalhes.

## 5 de maio de 2015: atualizado o buildpack do Node.js v1.17-20150429-1033

* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Se o aplicativo não especificar um tempo de execução em seu arquivo
package.json, o app agora será iniciado usando v0.12.1, em vez de v0.10.x. Se for
necessário usar a versão anterior, especifique v0.10.x no package.json conforme
mostrado.

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Problemas conhecidos com a v0.12.1:
   * O recurso “Suspender” é interrompido quando você usa o recurso Ferramenta de depuração fornecido pelo Bluemix Live Sync.
   * O módulo mqlight usado para o serviço MQ Light não é suportado na v0.12.x

* Foram resolvidas várias vulnerabilidades de segurança:
  * Vulnerabilidades corrigidas em OpenSSL que afetam IBM SDK for Node.js. Mais detalhes estão disponíveis no [boletim de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnerabilidade corrigida em RC4 Stream Cipher que afetam IBM SDK for Node.js. Mais detalhes estão disponíveis no [boletim de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 de abril de 2015: atualizado o buildpack do Node.js v1.15-20150331-2231

* O buildpack Node.js agora inclui três novos recursos para ajudar a desenvolver rapidamente no Bluemix como faria na área de trabalho, sem reimplementação
  * Sincronização da Área de Trabalho: Sincronize qualquer árvore da área de trabalho (Windows) para uma área de trabalho do projeto baseado em nuvem
  * Edição em tempo real: permite que você faça mudanças em um aplicativo Node.js que é executado no Bluemix e teste-as imediatamente em seu navegador.
  * Depuração: Execute shell em seu ambiente e depure! É possível editar o código dinamicamente, inserir pontos de interrupção, percorrer o código, reiniciar o tempo de execução e muito mais, usando o depurador Node Inspector
  * Consulte [Gerenciamento de App](/docs/manageapps/app_mng.html#Utilities) para obter mais informações.
* Nós obtivemos as mudanças mais recentes do [buildpack do Node.js do Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Essa mudança vem com várias correções de erro e melhorias feitas pela comunidade.
* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 de janeiro de 2015: atualizado o buildpack do Node.js v1.9.1-20141208-1221

* O buildpack Node.js agora inclui suporte de configuração de log dinâmico. Com esse suporte, os desenvolvedores poderão mudar o nível de log de seus aplicativos dinamicamente se o aplicativo estiver usando os módulos log4js, bunyan ou ibmbluemix para criação de log.
* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Essa atualização inclui correções para o problema POODLE.

## 23 de outubro de 2014: atualizado o buildpack do Node.js v1.6-20141013-1736

* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Essa atualização significa que você obtém um tempo de execução do IBM Node.js totalmente suportado quando especifica o tempo de execução do Node.js estável mais recente para seu aplicativo, v0.10.32. Esse SDK mais recente é fornecido com uma correção para um problema com o módulo qs integrado que resultou em uma negação de serviço. Ele contém também uma versão atualizada do módulo npm e outros aprimoramentos nos módulos http e url. Para obter mais detalhes, consulte o [Log de mudanças v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* O buildpack contém também uma correção de um erro que estava incluindo um arquivo index.html incorreto no aplicativo do cliente durante a implementação.

## 30 de setembro de 2014: atualizado o buildpack do Node.js v1.4-20140908-1746

* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Essa atualização significa que você obtém um tempo de execução do IBM Node.js totalmente suportado quando especifica o tempo de execução do Node.js estável mais recente para seu aplicativo, v0.10.31. Com um tempo de execução do Node.js totalmente suportado, os clientes recebem uma experiência de suporte consistente.
* O buildpack contém uma estrutura de serviço melhorada. Especificamente, ele funciona melhor ao ligar o serviço Monitoramento e Analítica e fornece mais informações de diagnóstico se o serviço falha.

## 28 de agosto de 2014: atualizado o buildpack do Node.js v1.3-20140821-1143

* Agora, o buildpack Node.js mais novo vem com o IBM SDK for Node.js v1.1.0.6. Essa atualização significa que você obterá um tempo de execução do IBM Node.js totalmente suportado ao especificar o tempo de execução do Node.js estável mais recente, v0.10.30, para seu aplicativo. Esse tempo de execução corrige a [vulnerabilidade Dano à memória V8![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* O buildpack também inclui melhorias e correções de bug na extensão de serviço de
Monitoramento e Analítica, permitindo diagnosticar condições de desempenho e
erro por meio do serviço.

## 29 de julho de 2014: atualizado o buildpack do Node.js v1.1-20140717-1447

Agora, o buildpack Node.js vem com o IBM SDK for Node.js v1.1.0.5. Essa atualização significa que você obterá um tempo de execução do IBM Node.js totalmente suportado ao especificar o tempo de execução do Node.js estável mais recente para seu aplicativo, v0.10.29. Veja mais sobre os [IBM Node.js SDKs](https://developer.ibm.com/node/sdk/).

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do node.js](index.html)
