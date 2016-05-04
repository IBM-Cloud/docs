---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Atualizações mais recentes para o buildpack sdk-for-nodejs
{: #latest_updates}

*Última atualização: 22 de março de 2016*

Uma lista das atualizações mais recentes no buildpack sdk-for-nodejs.
## 29 de abril de 2016: atualizado o buildpack Node.js v3.3-20160418-1749

Esta liberação do buildpack inclui o tempo de execução do IBM SDK for Node.js versões 0.10.44, 0.12.13, 4.4.1 e 4.4.2. O padrão é agora 4.4.2. Várias versões de runtime anteriores do IBM SDK for Node.js também foram removidas. O buildpack agora inclui somente as duas versões mais recentes 0.10.x, 0.12.x e 4.x que são atualmente a 0.10.43, 0.10.44, 0.12.12, 0.12.13, 4.4.1 e 4.4.2.

Para 4.4.1 e 4.4.2, agora é possível usar uma versão compatível com FIPS do tempo de execução configurando a variável de ambiente `FIPS_MODE=true` para seu app. Em seguida, verifique `FIPS_MODE` na saída temporária para confirmar se ela foi reconhecida pelo buildpack.

O buildpack atualizado e as novas versões de runtime também contêm correções para vulnerabilidades de segurança:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

O buildpack atualizado contém correções para dois erros:
* Agora as construções do IBM SDK for Node.js serão sempre usadas se houver uma disponível correspondente ao intervalo solicitado. Anteriormente isso era verdadeiro somente para versões de runtime 4.x.
* Agora o utilitário do inspetor de gerenciamento de app funcionará com as versões de runtime 4.x.

## 18 de março de 2016: Atualizado o Buildpack Node.js v3.2-20160315-1257

Esta liberação do buildpack move o tempo de execução padrão do IBM SDK for Node.js da versão 4.3.0 para 4.3.2. Também inclui o IBM SDK for Node.js versões 0.10.43, 0.12.12 e 4.3.1. Os usuários devem usar essas versões recentes do Node.js para captar as correções para vulnerabilidades de segurança diversas.

## 4 de março de 2016: Atualizado o buildpack Node.js v3.1-20160222-1123

Esta liberação do buildpack move o tempo de execução padrão do IBM SDK for Node.js da versão 4.2.4 para 4.3.0. Também inclui o IBM SDK for Node.js versões 0.10.42, 0.12.10 e 4.2.6. Os usuários devem usar essas versões recentes do Node.js para captar as correções para vulnerabilidades de segurança diversas.

## 4 de fevereiro de 2016: Atualizado o buildpack Node.js v3.0-20160125-1224

Esta liberação é totalmente sincronizada com o buildpack do [Node.js da comunidade do Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Além de mudanças da comunidade, houve mudanças em determinados padrões, otimizações para reduzir o tempo de preparação e atualizações para o recurso App Management.

* Atualizações do buildpack:

  * O Node.js v4.2.4 (IBM SDK for Node.js Versão 4) agora é o tempo de execução padrão no Bluemix, substituindo o v0.12.9. Isso pode fazer com que seu aplicativo se comporte de forma diferente se você não tiver especificado uma determinada versão para seu aplicativo. Para saber como especificar uma versão do Node.js para seu aplicativo Bluemix, veja a documentação [Tempo de execução do Node.js](index.html).

  * NODE_ENV está agora configurado como *production* por padrão. Isso fará com que algumas dependências do nó se comportem de forma diferente. Por exemplo, a estrutura Express não retornará mais os rastreios de pilha no navegador da web para os terminais com falha, mas, em vez disso, exibirá apenas *Erro interno do servidor*. Quando NPM_CONFIG_PRODUCTION for configurado como *true*, o NPM configurará NODE_ENV como *production* para scripts subshell somente na fase de instalação do npm. Esse permite que os usuários configurem NODE_ENV para outro valor como *development* para o tempo de execução do aplicativo. Para clareza, os scripts npm verão a mensagem **NODE_ENV=production**.

  * Uma correção de bug para o serviço Monitoring and Analytics está incluída.

* Atualizações de armazenamento em cache:

  * Se o cache estiver desativado (NODE_MODULES_CACHE=false), o buildpack não tentará armazenar em cache nenhum módulo/componente. Anteriormente, essa configuração fazia isso para que o cache não estourasse, mas ainda armazenava em cache os módulos instalados para implementações futuras. Agora, ela nem estourará o cache nem tentará armazenar qualquer cache.

  * Bower_components são armazenados em cache por padrão, além de node_modules.

* Outras atualizações:

  * Avisos úteis foram incluídos para dependências ausentes como gulp, bower e angular.

  * O script de detecção é atualizado com as informações da versão do buildpack.

  * A recomendação de armazenamento em cluster (WEB_CONCURRENCY) introduzida inicialmente pela comunidade foi removida porque a determinação de memória era inexata no Bluemix.


## 16 de dezembro de 2015: Buildpack Node.js Atualizado v2.8-20151209-1403 e v3.0beta-20151211-2041

Esta liberação do buildpack Node.js é fornecida com duas versões, v2.8 e v3.0beta. Ambas as versões incluem as mudanças a seguir:

Uma Correção de bug para o serviço de Monitoramento e Analítica
A inclusão de um tempo de execução armazenado em cache para o IBM SDK para Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 e v1.2.0.7 (com base na comunidade Node.js v4.2.3, v4.2.2, v0.12.9 e v0.12.8, respectivamente)
Além do v3.0beta, o tempo de execução Node.js padrão é mudado para v4.2.3.

O IBM Node.js Buildpack v3.0beta foi liberado como um buildpack não padrão no Bluemix com Node.js v4.2.3 como o tempo de execução padrão. Para assegurar que seus apps e serviços continuarão funcionando no Bluemix, envie por push seu aplicativo com a versão beta do buildpack. Após 30 dias ou mais, v3 se tornará o buildpack padrão.

Para enviar por push seu aplicativo com v3.0beta:
* Use a opção "-b" em seu comando 'cf push':

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Ou, use a opção "buildpack" em seu arquivo manifest.yml:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Essa mudança para o tempo de execução padrão não afetará seu aplicativo se você tiver configurado uma versão específica do
Node.js no package.json de seu aplicativo. Observe que sempre é possível especificar a versão do Node.js para executar seu aplicativo usando a entrada engines.node em seu package.json conforme explicado em [Versões disponíveis](index.html#available_versions).

## 23 de novembro de 2015: Atualizado o buildpack Node.js v2.7-20151118-1003

Com o 2.7, incluímos a versão 4.2.1.0 do IBM SDK para Node.js (baseado em Node v4.2.1 LTS). Ele ainda não é o padrão, mas pode ser especificado para uso. Observe que
isso substitui a construção de software livre que estava disponível anteriormente. Também
fizemos algumas pequenas correções de bug para nossa estrutura de extensão de serviço.

## 19 de outubro de 2015: Atualizado o buildpack Node.js v2.6.1-20151015-1326

O Node.js v2.6.1 apresenta uma correção de bug para o [Manipulador de gerenciamento do app StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) e uma versão mais consistente de NPM.

## 15 de outubro de 2015: Atualizado o buildpack Node.js v2.6-20151006-1309

Esta liberação do buildpack Node.js apresenta a integração do [Gerenciador de processos StrongLoop](https://strong-pm.io) para o
recurso de Gerenciamento de app. Para obter mais informações, consulte a postagem do blog [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 de junho de 2015: Atualizado o buildpack Node.js v2.0-20150608-1503

Nessa liberação, sincronizamos nosso buildpack Node.js com o mais recente [Buildpack Node.js da comunidade CF](https://github.com/cloudfoundry/nodejs-buildpack), que é fornecido com inúmeros novos recursos da comunidade.
Além disso, reforçamos o recurso Gerenciamento de app no buildpack Node.js, que permite utilitários como
shell, node-inspector, Bluemix Live Sync e mais. Consulte [Gerenciamento de App](../../manageapps/app_mng.html) para obter detalhes.

## 5 de maio de 2015: Atualizado o buildpack Node.js v1.17-20150429-1033

* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Se seu aplicativo não especificar um tempo de execução em seu arquivo package.json, seu app agora será iniciado usando
v0.12.1, em vez de v0.10.x. Se for necessário usar a versão anterior, especifique v0.10.x em seu package.json conforme mostrado abaixo

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Existem problemas conhecidos com o v0.12.1:
   * Ao usar o recurso Debug Tools fornecido pelo Bluemix Live Sync, o recurso “Suspender” será quebrado.
   * O módulo mqlight usado para o serviço MQ Light não é suportado na v0.12.x

* Foram resolvidas várias vulnerabilidades de segurança:
  * Vulnerabilidades corrigidas em OpenSSL que afetam IBM SDK for Node.js. Mais detalhes estão disponíveis no [boletim de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnerabilidade corrigida em RC4 Stream Cipher que afetam IBM SDK for Node.js. Mais detalhes estão disponíveis no [boletim de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 de abril de 2015: Atualizado o buildpack Node.js v1.15-20150331-2231

* O buildpack Node.js agora inclui três novos recursos para ajudar a desenvolver rapidamente no Bluemix como faria na área de trabalho, sem reimplementação
  * Sincronização da Área de Trabalho: Sincronize qualquer árvore da área de trabalho (Windows) para uma área de trabalho do projeto baseado em nuvem
  * Edição em Tempo Real: É possível fazer mudanças em um aplicativo Node.js executando no Bluemix e testá-las imediatamente em seu navegador.
  * Depuração: Execute shell em seu ambiente e depure! É possível editar o código dinamicamente,
inserir pontos de interrupção, percorrer o código, reiniciar o tempo de execução e muito mais usando o depurador Node
Inspector
  * Consulte [Gerenciamento de App](../../manageapps/app_mng.html#Utilities) para obter mais informações.
* Executamos pull nas mais recentes mudanças do [Buildpack Node.js do Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Isso vem com
inúmeras correções de bug e melhorias feitas pela comunidade.
* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 de janeiro de 2015: Atualizado o buildpack Node.js v1.9.1-20141208-1221

* O buildpack Node.js agora inclui suporte de configuração de log dinâmico. Com isso, os desenvolvedores
pode mudar o nível de log de seus aplicativos em trânsito se o aplicativo estiver usando os módulos log4js,
bunyan ou ibmbluemix para criação de log.
* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Isso inclui
correções para o problema POODLE.

## 23 de outubro de 2014: buildpack do Node.js atualizado v1.6-20141013-1736

* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Isso significa que você obtém um tempo de execução do IBM Node.js totalmente suportado ao especificar o tempo de execução Node.js estável mais recente para seu aplicativo, v0.10.32. Esse SDK mais recente é fornecido com uma correção para um problema com o módulo qs integrado que resultou em uma negação de serviço. Ele contém também uma versão atualizada do módulo npm e outros aprimoramentos nos módulos http e url. Para obter detalhes adicionais, consulte o [Log de mudanças v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* O buildpack contém também uma correção de um erro que estava incluindo um arquivo index.html incorreto no aplicativo do cliente durante a implementação.

## 30 de setembro de 2014: buildpack Node.js atualizado v1.4-20140908-1746

* Agora, o buildpack Node.js vem com o [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Isso significa que você obterá um tempo de execução do IBM Node.js totalmente suportado ao especificar o tempo de execução Node.js estável mais recente para seu aplicativo, v0.10.31. Com o tempo de execução Node.js totalmente suportado, os clientes poderão construí-lo na parte superior sabendo que podem contar com o mesmo suporte detalhado que sempre tiveram para produtos IBM.
* O buildpack contém uma estrutura de serviço melhorada. Especificamente,
ele funciona melhor ao ligar o serviço Monitoring and Analytics
e fornece informações de diagnóstico adicionais no caso de falhas.

## 28 de agosto de 2014: buildpack Node.js atualizado v1.3-20140821-1143

* Agora, o buildpack Node.js mais novo vem com o IBM SDK for Node.js v1.1.0.6. Isso significa que você obterá um tempo de execução IBM Node.js totalmente suportado ao especificar o tempo de execução Node.js estável mais recente, v0.10.30, para seu aplicativo. Esse tempo de execução corrige a
[ vulnerabilidade de dano à memória V8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* O buildpack também inclui melhorias e correções de bug na extensão de serviço de
Monitoramento e Analítica, permitindo diagnosticar condições de desempenho e
erro por meio do serviço.

## 29 de julho de 2014: buildpack Node.js atualizado v1.1-20140717-1447

Agora, o buildpack Node.js vem com o IBM SDK for Node.js v1.1.0.5. Isso significa que você obterá um tempo de execução IBM Node.js totalmente suportado ao especificar o tempo de execução Node.js estável mais recente para seu aplicativo, v0.10.29. Veja mais sobre os IBM Node.js SDKs [aqui](https://developer.ibm.com/node/sdk/).

# rellinks
## geral
* [Tempo de execução do node.js](index.html)
