---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Definindo Políticas
{: #criteria}

Com o {{site.data.keyword.DRA_short}} é fácil definir as políticas para o seu aplicativo. Para
iniciar, siga estas etapas:
{:shortdesc}

1. No menu lateral, clique em **Política**.

2. Clique em **Criar política (+)** e, em seguida, insira um nome e uma descrição para a nova política.

3. Clique em **Avançar**.

4. Inclua pelo menos uma regra na política:
  1. Clique em **Criar regra (+)**.
  2. Selecione o tipo de regra.
  3. Insira detalhes e condições para a regra.
  4. Clique em **Salvar**.

5. Ao concluir a inclusão de regras na política, clique em **Concluído**.

As políticas são criadas na organização do {{site.data.keyword.Bluemix_notm}} à qual o {{site.data.keyword.DRA_short}} foi incluído. Qualquer
aplicativo que estiver na mesma organização poderá usar a política.

O {{site.data.keyword.DRA_short}} suporta estes tipos de métricas e formatos:

* Teste de verificação funcional (Mocha, JUnit)
* Teste de unidade (Mocha, JUnit, Karma/Mocha)
* Cobertura de código (Istanbul como formato do relatório de resumo de JSON, Blanket.js)

O {{site.data.keyword.DRA_short}} também suporta testes do Selenium e Jasmine. Esses testes devem ser incluídos dentro das ferramentas oficialmente
suportadas, como JUnit, xUnit e Mocha. Para saber mais sobre como usar o {{site.data.keyword.deliverypipeline}}, o {{site.data.keyword.DRA_short}} e o
Selenium juntos, consulte [Executando testes
do Selenium a partir da linha de comandos em um pipeline de entrega](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Para itens que têm casos de teste, é possível especificar casos de teste críticos, que são testes que devem passar independentemente da porcentagem
aceitável. Os nomes de casos de teste críticos devem corresponder ao atributo `full title` do caso de teste:    
* Para testes Karma/Mocha, as sequências de descrição `describe()` e `it()` são vinculadas com espaços
* Para testes JUnit, o nome do pacote, o nome de classe e o nome da função são vinculados com espaços    

É possível usar o Sauce Labs com o {{site.data.keyword.DRA_short}} incluindo a integração do Sauce Labs em seu pipeline. Em seguida, incorpore as
variáveis de ambiente `SAUCE_USERNAME` e `SAUCE_ACCESS_KEY` em testes do Selenium como credenciais.

É possível ver os títulos integrais nos logs após uma execução.  

Observações:
* O {{site.data.keyword.DRA_short}} não suporta testes críticos que contenham um hífen no título integral.    
* Se você mudar o seu nome da organização, deverá recriar as políticas que estavam associadas com o nome anterior. Você perderá o acesso a relatórios de decisão que foram gerados antes da mudança de nome.

## Criando regras de teste de verificação funcional
{: #criteria_fvt}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


## Criando regras de teste de unidade
{: #criteria_ut}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


## Criando regras de cobertura de código
{: #criteria_codecoverage}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de cobertura de código que é necessária para ser declarada bem-sucedida.

3. Para monitorar para regressões de cobertura de código, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

4. Clique em **Salvar**.
