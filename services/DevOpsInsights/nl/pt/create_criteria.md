---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Definindo Políticas
{: #policies}

As políticas controlam as portas em seu pipeline de entrega contínua. Se o seu código não atender nem exceder uma política executada em uma porta específica, a implementação será interrompida para evitar que as mudanças de risco sejam liberadas.
{:shortdesc}

As políticas são definidas no {{site.data.keyword.DRA_short}}. As políticas são criadas na organização (org.) do {{site.data.keyword.Bluemix_notm}} que contém o {{site.data.keyword.DRA_short}}. Qualquer aplicativo que estiver na mesma organização poderá usar a política. 

Para definir uma política:

1. Na navegação à esquerda, clique em **Configurações**.

2. Clique em **Política**.

3. Clique em **Criar política** e, em seguida, digite um nome e uma descrição para a nova política.

4. Clique em **Avançar**.

4. Inclua pelo menos uma regra na política:
  1. Clique em **Incluir regra na política**.
  2. Selecione o tipo de regra.
  3. Insira detalhes e condições para a regra.
  4. Clique em **Salvar**.

5. Ao concluir a inclusão de regras na política, clique em **Concluído**.

## Criando regras
{: #criteria}

As regras definem os critérios que suas políticas usam para julgar o sucesso ou a falha. É possível criar uma política "Teste de unidade e Cobertura de teste" que contenha uma regra de teste de unidade que requeira um sucesso de 80% de teste de unidade e uma regra de cobertura de teste que requeira 100% de cobertura de código. Se você incluir uma porta que se refira a essa regra em um pipeline, a porta evitará que quaisquer construções que não satisfaçam a ambas as regras continuem. 

É possível requerer o sucesso sem importar o quê marcando os testes como críticos. Para criar uma regra, selecione uma política e, em seguida, clique em **Incluir regra na política**. 

### Criando regras de teste de verificação funcional
{: #criteria_fvt}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar regressões de caso de teste, marque a caixa de seleção **Monitorar regressão de caso de teste**.

5. Clique em **Salvar**.


### Criando regras de teste de unidade
{: #criteria_ut}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar regressões de caso de teste, marque a caixa de seleção **Monitorar regressão de caso de teste**.

5. Clique em **Salvar**.


### Criando regras de cobertura de código
{: #criteria_codecoverage}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de cobertura de código que é necessária para ser declarada bem-sucedida.

3. Para monitorar regressões de cobertura de código, marque a caixa de seleção **Monitorar regressão de caso de teste**.

4. Clique em **Salvar**.

### Criando regras de varredura de segurança estática
{: #criteria_static}

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

### Criando regras de varredura de segurança dinâmica
{: #criteria_dynamic}

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

## Formatos e ferramentas de resultado de teste

O {{site.data.keyword.DRA_short}} suporta estes tipos de métricas e formatos:

* Teste de verificação funcional (Mocha, xUnit)
* Teste de unidade (Mocha, xUnit, Karma/Mocha)
* Cobertura de código (Istanbul como formato do relatório de resumo de JSON, Blanket.js)

O {{site.data.keyword.DRA_short}} também suporta testes do Selenium e Jasmine. Esses testes devem ser incluídos dentro das ferramentas oficialmente suportadas, como xUnit e Mocha. Para saber mais sobre como usar o {{site.data.keyword.deliverypipeline}}, o {{site.data.keyword.DRA_short}} e o Selenium juntos, veja [Executando testes do Selenium por meio da linha de comandos em um pipeline de entrega](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Para itens que têm casos de teste, é possível especificar casos de teste críticos, que são testes que devem passar independentemente da porcentagem
aceitável. Os nomes de casos de teste críticos devem corresponder ao atributo `full title` do caso de teste.    
* Para testes Karma/Mocha, as sequências de descrição `describe()` e `it()` são vinculadas aos espaços.
* Para testes xUnit, o nome do pacote, o nome de classe e o nome da função são vinculados aos espaços. Isso é ilustrado no seguinte exemplo:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Esse exemplo produz estes nomes de casos de teste:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

É possível usar o Sauce Labs com o {{site.data.keyword.DRA_short}} incluindo a integração de ferramenta do Sauce Labs em seu pipeline. Em seguida, incorpore as
variáveis de ambiente `SAUCE_USERNAME` e `SAUCE_ACCESS_KEY` em testes do Selenium como credenciais.

É possível ver os títulos completos de todos os testes nos logs após uma execução.  

**Observações:**
* O {{site.data.keyword.DRA_short}} não suporta testes críticos que contenham um hífen no título integral.    
* Se você mudar o seu nome da organização, deverá recriar as políticas que estavam associadas com o nome anterior. Você perderá o acesso a quaisquer relatórios de decisão que foram gerados antes da mudança de nome.

## Visualizando relatórios de decisão    
{: #DI_decision_reports}

Após um pipeline ser executado, o {{site.data.keyword.DRA_short}} começa a coletar e analisar os resultados de teste a partir dele, para estabelecer uma referência. Dados de cada execução subsequente são coletados e comparados com resultados anteriores. Portas de decisão usam esses dados para determinarem quando
parar uma implementação. 

Para visualizar o relatório de decisão para uma porta a partir do pipeline, conclua estas etapas:

   1. No estágio que contém a porta a ser verificada, clique em **Visualizar logs e histórico**.

   2. Na tarefa que contém a porta, clique no nome da porta.

   3. Na visualização de log, localize a mensagem `Verifique o relatório do {{site.data.keyword.DRA_short}} aqui` e clique no link para abrir o relatório.
