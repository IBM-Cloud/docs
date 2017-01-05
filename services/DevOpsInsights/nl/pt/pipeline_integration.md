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

# Integrando o {{site.data.keyword.DRA_short}} ao {{site.data.keyword.deliverypipeline}}
{: #toolchain_configure_pipeline}

Após incluir o {{site.data.keyword.DRA_full}} em uma cadeia de ferramentas e definir as políticas que ele monitora, deve-se, então, integrar o {{site.data.keyword.DRA_short}} com o seu pipeline.
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## Preparando estágios de pipeline para o {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_props}

Deve-se criar várias propriedades do ambiente em cada estágio de pipeline que contém tarefas de construção ou implementação:

1. Clique em **Configuração de estágio** e, em seguida, em **Configurar estágio**.

2. Clique em **PROPRIEDADES DO AMBIENTE**.

3. Inclua as três propriedades de texto a seguir e, em seguida, salve as mudanças no estágio:

<table><thead>
<tr>
<th>Propriedade do ambiente</th>
<th>Descrição</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>O nome do app como aparece nos painéis do {{site.data.keyword.DRA_short}}. </td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>O nome do ambiente no qual o app está em execução. Essa propriedade é usada para categorizar o app em painéis do {{site.data.keyword.DRA_short}}.</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>Um prefixo que é incluído em construções conforme mostrado em painéis do {{site.data.keyword.DRA_short}}.</td>
</tr>
</tbody></table>


## Atualizando tarefas de teste para o {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_upload}

Para iniciar, recupere as informações de configuração a partir de uma tarefa de teste.

1. No estágio que contém uma tarefa de teste, clique no ícone **Configuração de estágio**
![Ícone Configuração de estágio de pipeline](images/pipeline-stage-configuration-icon.png). Clique em **Configurar
estágio**.
2. Crie uma atividade. Para o tipo de tarefa, selecione **Teste**.
3. Selecione uma tarefa de teste que usa o tipo de Testador simples e copie as informações que estiverem nos campos de **Comando de teste**
e de **Diretório ativo** para um editor. Você precisará dessas informações posteriormente.
4. A partir da mesma Tarefa de teste simples, mude o tipo de testador selecionando **Testador avançado**.
5. No campo **Comando de teste**, cole os comandos que você copiou do campo **Comando de teste** da
tarefa de Teste simples.
6. No campo **Diretório ativo**, cole o caminho que você copiou do campo **Diretório ativo** da
tarefa de Teste simples.
7. Preencha os campos restantes para fazer upload dos resultados de teste para um tipo de teste específico. Se você deseja fazer upload dos resultados para um
segundo tipo de teste na mesma tarefa, também preencha os campos que são prefixadas com *Adicional*.

 * Tipo de métrica
 * Formato
 * Local do arquivo de resultado
8. Clique em **Salvar** para retornar para o pipeline.

Os valores para os campos de **Tipo de métrica** e de **Local do arquivo de resultado** devem corresponder ao formato
correto:

<table><thead>
<tr>
<th>Tipo de métrica</th>
<th>Formatos suportados</th>
</tr>
</thead><tbody>
<tr>
<td>Teste de verificação funcional</td>
<td>Mocha, JUnit</td>
</tr>
<tr>
<td>Teste unitário</td>
<td>Mocha, JUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Cobertura do Código</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

A *Figura 1* mostra uma tarefa de teste que está configurada para executar testes de unidade; faça upload dos resultados no formato Mocha e faça
upload dos resultados da cobertura de código em formato Istanbul.

![Tarefa de upload de Analítica de risco de implementação](images/DRA_upload_job.png)
*Figura 1. Resultados de upload para o DevOps Analytics*

## Definindo portas do {{site.data.keyword.DRA_short}} no pipeline
{: #toolchain_pipeline_gates}

Portas do {{site.data.keyword.DRA_short}} verificam se os seus resultados do teste obedecem à política definida. Se a política não for atendida, a porta
do {{site.data.keyword.DRA_short}} falhará. Geralmente, as portas são colocadas no término de cada estágio de seu pipeline. Esse local é ideal para verificar a qualidade da construção com relação à sua política, para assegurar
que ela é segura para ser promovida de um ambiente para outro. No entanto, é possível
colocar portas em qualquer lugar no pipeline nas quais você deseja que um critério específico seja verificado.

1. Em um estágio, clique no ícone **Configuração de estágio** ![Ícone Configuração
de estágio de pipeline](images/pipeline-stage-configuration-icon.png) e clique em Configurar estágio.
2. Clique em **Incluir Tarefa**. Para o tipo de tarefa, selecione **Teste**.
3. Insira um nome para a nova tarefa, como *Porta (Teste de unidade)*.
4. Para tipo de testador, selecione **Porta do {{site.data.keyword.DRA_short}}**.
5. Especifique o nome do ambiente. Certifique-se de que esse valor corresponda ao que foi definido em suas
[propriedades do ambiente](#toolchain_pipeline_props).
6. Defina o nome da política que deve ser verificada nessa porta.

 Esse nome deve corresponder exatamente a um dos nomes de política que você definiu. É possível especificar apenas políticas que são definidas na mesma
organização do {{site.data.keyword.Bluemix_notm}} que a sua cadeia de ferramentas.

7. Opcional: para fazer uma função de porta no modo consultivo, limpe a caixa de seleção **Parar a execução deste estágio se essa tarefa
falhar**. Em modo consultivo, o {{site.data.keyword.DRA_short}} conclui a mesma análise de política na porta e gera relatórios, mas, se uma falha
ocorrer, o pipeline não será parado.
8. Clique em **Salvar** para retornar para o pipeline.
9. Configure portas para todas as suas políticas do {{site.data.keyword.DRA_short}} repetindo estas etapas.

![Tarefa Mocha de analítica de risco de implementação](images/DRA_gate_job.png)
*Figura 2. Porta do DevOps Analytics*

Após o seu pipeline estar configurado, comece a usar o {{site.data.keyword.DRA_short}}. Para obter instruções, consulte
[Executando o pipeline de entrega](./pipeline_decision_reports.html#toolchain_reports).
