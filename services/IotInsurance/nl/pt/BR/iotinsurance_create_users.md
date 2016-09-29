---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Criando associações de usuários e blindagem
{: #gettingstartedtemplate}
Última atualização: 12 de setembro de 2016
{: .last-updated}

Depois de criar o serviço {{site.data.keyword.iotinsurance_short}} e implementar os serviços de apoio e os apps necessários, é possível testar o serviço criando um usuário autorizado e uma associação de proteção.
{:shortdesc}

**Pré-requisitos:** antes de iniciar, assegure-se de que os pré-requisitos a seguir estejam adequados:

- [Node.js](https://nodejs.org/en/) instalado no computador.  
- Um ambiente de tempo de execução ativado para Node.js, como o Eclipse.
- Software Git e acesso ao [Repositório de código-fonte GitHub para os exemplos de API](https://github.com/ibm-watson-iot/ioti-samples).   Como alternativa, é possível fazer download do [archive com os arquivos de código-fonte](https://github.com/ibm-watson-iot/ioti-samples/archive/master.zip).
- Código-fonte preparado.
  Para preparar o código-fonte, conclua estas etapas:
  1. Clone ou faça download do [Repositório de código-fonte GitHub](https://github.com/ibm-watson-iot/ioti-samples) para seu computador.
  2. Instale os pré-requisitos de software livre do projeto usando um prompt de comandos para acessar a pasta que contém os arquivos de código-fonte clonados e executando o comando `npm install`.

Crie um usuário que possa ser usado para testar os recursos do painel e o app móvel de amostra.

1. Crie um usuário no sistema do {{site.data.keyword.iotinsurance_short}}.
  1. Edite o arquivo createUser.js para substituir os valores na variável **user** por informações exclusivas sobre o usuário.
  2. Salve o arquivo.
  3. Execute `node createUser.js`. O processo leva alguns momentos para ser concluído.
  4. Anote o nome do usuário; ele será necessário na próxima etapa.
2. Crie uma associação de proteção para o usuário.
  1. Edite o arquivo createUserShieldAssociation.js para incluir o nome do usuário da etapa anterior na variável **username**.
  2. Salve o arquivo.
  3. Execute `node createUserShieldAssociation.js`. Para obter mais informações sobre proteções, consulte [Componentes](iotinsurance_overview.html#components}).
3. (opcional) O mecanismo de análise é atualizado automaticamente, no entanto, se os dados corretos não forem exibidos, será possível atualizar o mecanismo de análise executando `node updateAnalyticsEngine.js`.
4. (opcional) Simule um evento de risco para o usuário.
  1. Edite o arquivo simulateHazard.js para incluir o nome do usuário das etapas anteriores na variável **usr**.
  2. Salve o arquivo.
  3. Execute `node simulateHazard.js`.
5. (opcional) Crie um conjunto de dados históricos simulados executando `node createHistoricalData.js`.


# Links Relacionados
{: #rellinks}

## Referência de API
{: #api}
* [Exemplos de API do {{site.data.keyword.iotinsurance_short}}](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Links Relacionados
{: #general}
* [Fórum de suporte do desenvolvedor](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Fórum de suporte do Stack overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
