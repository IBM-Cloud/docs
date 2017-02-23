---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conectando e configurando um serviço de historiador usando {{site.data.keyword.messagehub}}  
{: #messagehub_main}

Conectar o {{site.data.keyword.messagehub_full}} ao {{site.data.keyword.iot_short}} fornece um barramento de mensagem escalável, de alto rendimento para armazenamento de dados históricos. O {{site.data.keyword.messagehub}} é construído no Apache Kafka, que é um software livre, um sistema de mensagens de alto rendimento que fornece uma plataforma de baixa latência para a manipulação de feeds de dados em tempo real.

## Antes de iniciar  
{: #byb}

Antes de conectar um {{site.data.keyword.messagehub}} ao seu serviço {{site.data.keyword.iot_short}}, conclua as tarefas a seguir:

- Configure o {{site.data.keyword.messagehub}} no mesmo espaço do {{site.data.keyword.Bluemix_notm}} que o {{site.data.keyword.iot_short_notm}} usando o Catálogo do {{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre o {{site.data.keyword.messagehub}}, veja a [Introdução ao {{site.data.keyword.messagehub}} ![Ícone de link externo](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/MessageHub/index.html){: new_window}.

- Assegure-se de ter privilégios de desenvolvedor na organização do {{site.data.keyword.Bluemix_notm}} e de estar conectado por meio do {{site.data.keyword.Bluemix_notm}}. Se você não estiver conectado por meio do {{site.data.keyword.Bluemix_notm}} ou não tiver privilégios de desenvolvedor nessa organização do {{site.data.keyword.Bluemix_notm}}, você não será capaz de
autorizar a ligação do {{site.data.keyword.messagehub}} e o {{site.data.keyword.iot_short_notm}}.

## Conectar

Para conectar o {{site.data.keyword.messagehub}} ao armazenamento de dados históricos:

1. Em seu painel do {{site.data.keyword.iot_short}}, clique em **Extensões** na barra de navegação.
2. No quadro Armazenamento de dados históricos, clique em **Configurar**.
4. Selecione o serviço {{site.data.keyword.messagehub}} ao qual deseja se conectar.  
Todos os serviços disponíveis do {{site.data.keyword.messagehub}} dentro do mesmo espaço do {{site.data.keyword.Bluemix_notm}} que o seu serviço do {{site.data.keyword.iot_short}} são
listados na seção Configurar armazenamento de dados históricos.
5. Selecione as opções de configuração de seu {{site.data.keyword.messagehub}}:
 1. Selecione um fuso horário.  
 Os registros de data e hora nos dados do dispositivo que são enviados para o {{site.data.keyword.messagehub}} são convertidos para o fuso horário selecionado.
 2. Selecione um tópico padrão.  
 Os eventos de dispositivo serão enviados para o tópico padrão se um estiver definido aqui. Para usar designações de tópicos mais granulares, deixe o tópico padrão em branco e inclua regras customizadas de encaminhamento.
 3. Opcional: especifique regras customizadas de encaminhamento.  
 Especifique regras adicionais para eventos de dispositivo de encaminhamento. Somente os eventos que correspondem às regras customizadas de encaminhamento são encaminhados.  
 **Observação:** um evento pode corresponder a diversas regras de encaminhamento e será encaminhado para vários tópicos do {{site.data.keyword.messagehub}}.
 4. Opcional: configure os tópicos.  
 Para criar os tópicos com mais do que as duas partições padrão, é possível especificar a configuração da partição.
 5. Clique em **Pronto**.
5. Clique em **Autorizar**.
6. Na caixa de diálogo Autorização, clique em **Confirmar**.

Seu dispositivo de dados agora está armazenado em seu {{site.data.keyword.messagehub}}.
