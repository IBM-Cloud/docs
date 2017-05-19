---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Criando políticas e regras
{: #policies_and_rules}

As políticas são conjuntos de regras que controlam as portas em seu pipeline de entrega. Se o seu código não atender nem exceder uma política executada em uma porta específica, a implementação será interrompida para evitar que as mudanças de risco sejam liberadas.

As políticas são definidas no {{site.data.keyword.DRA_short}}. As políticas são criadas na organização (org.) do {{site.data.keyword.Bluemix_notm}} que contém o {{site.data.keyword.DRA_short}}. Qualquer aplicativo que estiver na mesma organização poderá usar a política. 

## Criando políticas
{: #create_policies}

Para criar uma política:

1. Na navegação à esquerda, clique em **Configurações**.

2. Clique em **Políticas**.

3. Clique em **Criar política** e, em seguida, digite um nome e uma descrição para a nova política.

4. Clique em **Avançar**.

4. Inclua pelo menos uma regra na política:
  1. Clique em **Incluir regra na política**.
  2. Selecione o tipo de regra.
  3. Insira detalhes e condições para a regra.
  4. Clique em **Salvar**.

5. Ao concluir a inclusão de regras na política, clique em **Concluído**.

## Criando regras
{: #creating_rules}

As regras definem os critérios que suas políticas usam para julgar o sucesso ou a falha. É possível criar uma política "Teste de unidade e Cobertura de teste" que contenha uma regra de teste de unidade que requeira um sucesso de 80% de teste de unidade e uma regra de cobertura de teste que requeira 100% de cobertura de código. Se você incluir uma porta que se refira a essa regra em um pipeline, a porta evitará que quaisquer construções que não satisfaçam a ambas as regras continuem. 

É possível requerer o sucesso sem importar o quê marcando os testes como críticos. Para criar uma regra, selecione uma política e, em seguida, clique em **Incluir regra na política**. 

### Criando regras de teste de verificação funcional
{: #criteria_fvt}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


### Criando regras de teste de unidade
{: #criteria_ut}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de casos de teste que devem passar para serem declarados como bem-sucedidos.

3. Defina qualquer caso de teste que seja crítico.

4. Para monitorar para regressões de caso de teste, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

5. Clique em **Salvar**.


### Criando regras de cobertura de código
{: #criteria_codecoverage}

1. Digite uma descrição e selecione um formato.

2. Especifique a porcentagem de cobertura de código que é necessária para ser declarada bem-sucedida.

3. Para monitorar para regressões de cobertura de código, selecione a caixa de seleção **Monitorar para regressão de caso de teste**.

4. Clique em **Salvar**.

### Criando regras de varredura de segurança estática
{: #criteria_static}

É possível integrar o {{site.data.keyword.DRA_short}} ao IBM Application Security on Cloud para executar varreduras de código estático e de app dinâmico. Para obter mais informações sobre o Application Security on Cloud, veja [a documentação oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.

### Criando regras de varredura de segurança dinâmica
{: #criteria_dynamic}

É possível integrar o {{site.data.keyword.DRA_short}} ao {{site.data.keyword.appseccloudfull}} para executar varreduras de apps dinâmicos. Para obter mais informações sobre o Application Security on Cloud, veja [a documentação oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Digite uma descrição.

2. Especifique os números máximos de problemas de alta, média e baixa gravidade que são permitidos pela regra. 

3. Clique em **Salvar**.
