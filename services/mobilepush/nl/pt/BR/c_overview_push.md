---

copyright:
 years: 2015, 2016

---

# Sobre {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Última atualização: 16 de agosto de 2016
{: .last-updated}

O IBM {{site.data.keyword.mobilepushshort}} é um serviço que pode ser usado para enviar notificações para dispositivos iOS e Android. É possível direcionar notificações para todos os usuários
do aplicativo ou para um conjunto específico de usuários e dispositivos usando tags. É possível administrar dispositivos, tags e assinaturas. É
possível também usar um SDK (kit de desenvolvimento de software) e interfaces de
programação de aplicativo (APIs) Representational State Transfer (REST) para
desenvolver ainda mais seus aplicativos cliente. 

O {{site.data.keyword.mobilepushshort}} também está disponível como um serviço Bluemix Dedicated. Para obter informações sobre o {{site.data.keyword.mobilepushshort}} como um serviço dedicado, consulte [Serviços dedicados](../../dedicated/index.html). Observe que a guia de monitoramento {{site.data.keyword.mobilepushshort}} não mostra dados de analítica.

O serviço {{site.data.keyword.mobilepushshort}} agora está ativado para OpenWhisk. Para obter mais informações, consulte [OpenWhisk](../../openwhisk/index.html).


## Processo do serviço {{site.data.keyword.mobilepushshort}}
{: #overview_push_process}

Os clientes móveis podem assinar e registrar-se para o serviço {{site.data.keyword.mobilepushshort}}. Na inicialização, os aplicativos móveis se registrarão e assinarão o serviço {{site.data.keyword.mobilepushshort}}. As notificações são
despachadas para o servidor Apple Push Notification Service (APNs) ou Google Cloud Messaging
(GCM) e, em seguida, enviadas para clientes móveis registrados.

![Visão geral de push](images/overview.jpg)


###Aplicativos Remotos
{: mobile-applications}

Na inicialização, os aplicativos móveis se registram e assinam o serviço {{site.data.keyword.mobilepushshort}} para receber notificações.

###Aplicativos backend
{: backend-applications}

Os aplicativos backend podem ser locais ou estarem em uma nuvem pública. Os aplicativos backend usarão o serviço {{site.data.keyword.mobilepushshort}} para enviar notificações sensíveis ao contexto para usuários móveis. Os aplicativos backend não são necessários para manter e gerenciar dispositivos móveis e informações sobre o usuário para enviar notificações push. Em vez disso, os aplicativos backend podem usar o serviço {{site.data.keyword.mobilepushshort}}.

###Proprietário backend do app
{: app-backend-owner}

O proprietário backend do App cria o aplicativo backend móvel que empacota uma instância do serviço {{site.data.keyword.mobilepushshort}}. O proprietário backend do App também configura e instala o serviço {{site.data.keyword.mobilepushshort}} para adequar os aplicativos backend usando o serviço junto a aplicativos móveis destinados para {{site.data.keyword.mobilepushshort}}.

###Serviço {{site.data.keyword.mobilepushshort}}
{: push-notification-service}

O serviço {{site.data.keyword.mobilepushshort}} gerencia todas as informações relacionadas a dispositivos registrados para notificações. O serviço mantém seus aplicativos transparentes para os detalhes de tecnologia de envio de notificações para plataformas móveis heterogêneas, manipulando tudo isso.

###Gateways
{: gateways}

Serviços de nuvem específicos da plataforma de dispositivo móvel como Google Cloud Messaging (GCM) ou Apple Push Notification Service (APNs) usam o serviço {{site.data.keyword.mobilepushshort}} para despachar notificações para os aplicativos móveis.

###Segurança de Push
{: push-security}

As APIs de {{site.data.keyword.mobilepushshort}} são asseguradas por dois tipos de segredos - i) appSecret ii) clientSecret.  O 'appSecret' protege APIs que são chamadas geralmente por aplicativos backend como a API para enviar {{site.data.keyword.mobilepushshort}}, a API de configuração para configurar definições.   O 'clientSecret' protege APIs que são chamadas geralmente por aplicativos cliente móveis.  No momento, há somente uma API relacionada para registro de um dispositivo com um UserId associado que requer esse 'clientSecret'. Todas as outras APIs chamadas a partir de clientes móveis não requerem o clientSecret. O 'appSecret' e o 'clientSecret' são alocados para todas as instâncias de serviço no momento da ligação de um aplicativo ao serviço {{site.data.keyword.mobilepushshort}}. Consulte a documentação da API REST para obter mais informações sobre como os segredos devem ser passados e para quais APIs.

## Tipos de {{site.data.keyword.mobilepushshort}}
{: #overview-push-types}

###Difusão
{: broadcast}

Quando um aplicativo móvel se registra com o serviço {{site.data.keyword.mobilepushshort}}, ele pode começar a receber transmissões. Notificações de transmissão são mensagens destinadas a todos os dispositivos que possuem um aplicativo instalado e configurado para o serviço {{site.data.keyword.mobilepushshort}}. As notificações de transmissão são ativadas por padrão para qualquer aplicativo ativado para {{site.data.keyword.mobilepushshort}}. Aplicativos ativados para o serviço {{site.data.keyword.mobilepushshort}} possuem uma assinatura predefinida para a tag Push.ALL, que é usada pelo servidor para transmitir mensagens de notificação para todos os dispositivos. Para enviar uma
notificação de transmissão usando a API Push REST, assegure-se de que
o "destino" seja um JSON vazio ao postar no recurso de mensagens.

###Notificações baseadas em tag
{: tag-based-notifications}

Notificações de tag são mensagens destinadas a todos os dispositivos inscritos em uma tag específica. As notificações baseadas em identificação
permitem a segmentação de notificações com base em áreas ou tópicos de assunto. Os destinatários da notificação podem optar por receber notificações somente se for
sobre um assunto ou um tópico de interesse. Portanto, a notificação baseada em
identificação fornece um meio de segmentar destinatários. Esse recurso ativa
a capacidade de definir identificações e, em seguida, de enviar e receber mensagens por identificações. Uma
mensagem é destinada somente aos dispositivos que assinaram uma identificação. Deve-se primeiramente criar tags para o aplicativo, configurar as assinaturas da tag e, em seguida, iniciar as notificações baseadas em tag. Para enviar uma notificação baseada em tag que usa a API REST, assegure-se de que os "tagNames" sejam fornecidos ao postar no recurso de mensagem.

###Notificações unicast
{: unicast-notifications}

Notificações unicast são mensagens destinadas a um dispositivo ou usuário específico. As notificações unicast destinadas a dispositivos não requerem configuração adicional e são ativadas por padrão quando o aplicativo está ativado para {{site.data.keyword.mobilepushshort}}.

No entanto, as notificações Unicast destinadas a usuários requerem:

- Associação de um ID do usuário a um dispositivo no momento do registro do dispositivo móvel para notificações push.  

- Autorização desse registro de ID do usuário passando um 'clientSecret' que é alocado ao ligar um aplicativo backend ao serviço {{site.data.keyword.mobilepushshort}}. 

Geralmente, um aplicativo móvel executará primeiro um ciclo de autenticação no qual o usuário do app móvel seja autenticado em um serviço de autenticação [como o Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Na autenticação bem-sucedida, o ID de usuário autenticado é então passado para a API do Registro de dispositivo push, junto a um clientSecret. A presença de um clientSecret utiliza apenas a associação autorizada de IDs do usuário a registros de dispositivo móvel.
Para enviar notificações Unicast por meio da API REST, assegure-se de que os deviceIds ou userIds sejam fornecidos ao postar em um recurso de mensagem.

###Notificações com base em plataforma
{: platform-based-notifications}

Notificações podem ser
destinada a atingir uma plataforma de dispositivo
específica. Por exemplo, uma notificação pode ser enviada a todos os
usuários do Android somente. Para enviar uma notificação baseada em
plataforma usando a API REST, assegure-se de que as plataformas
destinadas sejam fornecidas ao postar no recurso de mensagem. Especifique as plataformas como uma matriz. As plataformas
suportadas são como a seguir:
* A (Apple)
* G (Google)

## Tamanho da mensagem de {{site.data.keyword.mobilepushshort}}
{: #push-message-size}

O tamanho de carga útil da mensagem de {{site.data.keyword.mobilepushshort}} depende dos mediadores. 

###iOS
{: ios-message-size}

Para o iOS 8 e posterior, o tamanho máximo permitido é 2 kilobytes. O serviço de Notificação push Apple não envia notificações que excedem
esse limite.

###Android
{: android-message-size}

Não há limites na plataforma Android.
