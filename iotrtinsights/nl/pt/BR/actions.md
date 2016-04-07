---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Tipos de Ações {: #actions}

Além de exibir alertas no painel de alertas, o {{site.data.keyword.iotrtinsights_short}} suporta vários tipos de ações acionadas por regras, como enviar e-mails e enviar webhooks.
{: shortdesc}

## Criando Ações {: #shared}
É possível [criar ações diretamente a partir do editor de regras](rules.html "Criar regras") ou criar as ações no painel Ações e, em seguida, selecionar as ações ao criar suas regras.

Para criar uma ação a partir do painel Ações: 
1. No console do {{site.data.keyword.iotrtinsights_short}}, acesse **Análise > Ações**.
2. Clique em **Incluir nova ação**, selecione um tipo de ação, forneça um nome para a ação e forneça uma descrição. 
3. Forneça os parâmetros necessários para o tipo de ação que você está criando.
Tipos de ação:  
 - [Enviar e-mail](#email "Enviar e-mail")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. Clique em **OK** para criar a nova ação. 

A ação agora está disponível no [Editor de regras](rules.html#rules "Editor de regras"). 



## Enviar e-mail {: #email}
Use a ação enviar e-mail para enviar um e-mail para um ou mais destinatários quando uma regra for acionada. 

Exemplo: [Enviar e-mail](action_examples.html#emailex).

Os parâmetros a seguir são usados para configurar a ação enviar e-mail: 

Parâmetro | descrição
---|---
Name | O nome da ação, que é usado no Painel de alertas.
descrição | Uma breve descrição da ação.
To | Um ou mais endereços de e-mail, separados por vírgulas.
Cc | Um ou mais endereços de e-mail, separados por vírgulas.
Entidade | A linha de assunto do e-mail. Opcionalmente, é possível iniciar automaticamente o assunto com "Alerta do IoT Real-Time Insight".

O corpo do e-mail é criado automaticamente a partir da mensagem do dispositivo no momento em que a regra foi acionada.   
**Importante:** se os dados do dispositivo contiverem informações confidenciais, será possível optar por não incluir os dados do dispositivo no e-mail e mostrar os dados sensíveis somente no painel de alertas. 


## Webhook {: #webhook}
Use a ação do webhook para fazer uma solicitação de HTTP para um serviço da web ativado para o webhook quando um alerta for acionado. Por exemplo, um webhook poderia ser usado para abrir uma solicitação de serviço para um ativo se um sensor no dispositivo relatar uma leitura anormal. 

Exemplo: [Use o webhook para postar no Slack](action_examples.html#webhookex).

Os parâmetros a seguir são usados para configurar uma ação do webhook: 

Parâmetro | descrição
---|---
Name | O nome da ação, que é usado no painel Alertas.
descrição | Uma breve descrição da ação.
Localizador Uniforme de Recursos | A URL do servidor de destino ativado para o webhook. **Dica:** é possível usar a [substituição de variável](#variable_substitution) para incluir dados adicionais dinamicamente na URL.
Comunicação | O tipo de chamada do webhook a ser executada. Selecione um dos tipos a seguir: GET, HEAD, OPTIONS, PATCH, PUT, POST ou DELETE.
Nome de usuário | Inclua se necessário pelo serviço da web.
Senha | Inclua se necessário pelo serviço da web. **Importante:** a senha é enviada em texto não criptografado.
Cabeçalho | Os cabeçalhos são compostos de pares de chave e valor. **Dica:** é possível usar a [substituição de variável](#variable_substitution) para incluir dados adicionais dinamicamente no cabeçalho.
Tipo de conteúdo | O tipo de conteúdo do corpo: JSON, XML, URL codificada de formulário WWW ou texto simples. Disponível para os métodos OPTIONS, PATCH, PUT, POST e DELETE.
Conteúdo | O corpo da chamada do webhook. Disponível para os métodos OPTIONS, PATCH, PUT, POST e DELETE. Por padrão, o campo de corpo é preenchido previamente com todas as variáveis listadas em [substituição de variável](#variable_substitution). Selecione **Usar corpo da mensagem customizado** para editar o conteúdo do campo de corpo. **Importante:** O servidor webhook pode requerer que determinados campos específico sejam incluídos no corpo. Por exemplo, um webhook do Slack deve conter o campo "text".   



## Node-RED {: #nodered}
Use a ação do Node-RED para se conectar a um aplicativo Node-RED quando uma regra for acionada. Para obter mais informações sobre como usar o Node-RED, veja [Criando apps com o aplicativo iniciador Internet of Things](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500).

Exemplo: [Use o Node-RED para enviar uma mensagem de texto](action_examples.html#noderedex).

Os parâmetros a seguir são usados para configurar uma ação do Node-RED: 

Parâmetro | descrição
---|---
Name | O nome da ação, que é usado no painel Alertas.
descrição | Uma breve descrição da ação.
Localizador Uniforme de Recursos | A URL do nó de entrada HTTP Node-RED de destino.
Nome de usuário | Inclua se requerido pelo serviço Node-RED.
Senha | Inclua se requerido pelo serviço Node-RED. **Importante:** a senha é enviada em texto não criptografado.
Conteúdo | Por padrão, o campo de corpo é preenchido previamente com todas as variáveis listadas em [substituição de variável](#variable_substitution). Selecione **Usar corpo da mensagem customizado** para editar o conteúdo do campo de corpo.

## IFTTT {: #ifttt}
Use a ação IFTTT para acionar uma receita do IFTTT quando uma regra for acionada. Para obter mais informações sobre como acionar ações do Real-Time Insights como receitas do IFTTT, veja [Canal Maker](https://ifttt.com/maker) no site do IFTTT.

Exemplo: [Use o IFTTT para postar um cartão do Trello](action_examples.html#iftttex).

Os parâmetros a seguir são usados para configurar uma ação do IFTTT: 

Parâmetro | descrição
---|---
Name | O nome da ação, que é usado no painel Alertas.
descrição | Uma breve descrição da ação.
Key | A chave do Canal Maker a ser usada para acionar o evento.
As classes de eventos | O nome do evento que você configurou como um acionador para o Evento Maker. É possível criar várias receitas com diferentes acionadores, cada uma com um nome de evento diferente.
Valor de 1 a 3 | É possível passar qualquer conteúdo nesses parâmetros, que são passados para a ação em sua receita do IFTTT. **Dica:** é possível usar uma [substituição de variável](#variable_substitution) para incluir dados adicionais dinamicamente com o cabeçalho.

## Substituição de Variável {: #variable_substitution}
Inclua as substituições de variáveis a seguir para incluir dados do dispositivo dinamicamente. A variável deve ser agrupada em chaves duplas.

Variable | descrição
---|---
**URL, cabeçalho e corpo** |
`{{timestamp}}` | O registro de data e hora da mensagem
`{{tenantId}}` | O ID do serviço Real-Time Insights
`{{deviceId}}` | O ID do dispositivo
`{{ruleName}}` | O nome da regra que inclui a ação
**Somente corpo** |
`{{ruleDescription}}`| A descrição da regra que inclui a ação
`{{ruleCondition}}` | A condição da regra que acionou a ação
`{{message}}` | A mensagem do dispositivo bruto que incluiu o valor de ponto de dados que acionou a regra
