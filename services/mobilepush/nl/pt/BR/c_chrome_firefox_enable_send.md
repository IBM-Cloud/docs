---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enviando notificações básicas para navegadores da web
{: #web_notifications}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Depois de ter desenvolvido seus aplicativos, é possível enviar uma notificação push. 

1. Selecione **Enviar notificações** e componha uma mensagem escolhendo **Notificações da web** como a opção **Enviar para**. 
2. Digite a mensagem que precisa ser entregue no campo **Mensagem**.
3. É possível optar por fornecer configurações opcionais:
  - **Título da notificação**: esse é o texto que seria exibido como título de alerta de mensagem.
  - **URL do ícone de notificação**: se sua mensagem precisar ser entregue com um ícone de notificação de app, forneça o link para o ícone no campo.
  - **Tempo de vida**: notifica o servidor sobre a validade das mensagens.
4. Para notificações da web enviadas ao navegador Safari, há algumas informações adicionais necessárias:
  - **Ação**: este é o rótulo do botão de ação.
  - **Argumentos da URL**: os argumentos da URL que precisam ser usados com esta
notificação. Assegure-se de que isso seja fornecido na forma de uma matriz JSON. 
 
A imagem a seguir mostra a opção de notificações da web no painel.

  ![Tela de notificações](images/DashboardWebpush.jpg)


## Etapas Seguintes
  {: #next_steps_tags}

Após ter configurado com sucesso as notificações básicas,
será possível configurar notificações baseadas em tag e opções avançadas.

Inclua esses recursos de serviço do {{site.data.keyword.mobilepushshort}} no seu app. Para usar
notificações baseadas em tag, consulte [Notificações baseadas em
tag](c_tag_basednotifications.html). Para
usar opções de notificações avançadas, veja [Notificações avançadas](t_advance_badge_sound_payload.html).



