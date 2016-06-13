---

copyright:
 years: 2015, 2016

---

# Sobre notificações push
{: #overview-push}

Notificações push são um serviço que pode ser usado para enviar notificações para
dispositivos iOS e Android. É possível direcionar notificações para todos os usuários
do aplicativo ou para um conjunto específico de usuários e dispositivos usando tags. É possível administrar dispositivos, tags e assinaturas. É
possível também usar um SDK (kit de desenvolvimento de software) e interfaces de
programação de aplicativo (APIs) Representational State Transfer (REST) para
desenvolver ainda mais seus aplicativos cliente. Para obter
informações sobre o serviço dedicado de push, consulte
[Serviços dedicados](../../dedicated/index.html). 


## Processo do serviço de notificação push
{: #overview_push_process}

Clientes móveis podem assinar e se registrar no
Push Notification Service. Na inicialização, os aplicativos móveis
se registram e assinam o Push
                Notification Service. As notificações são
despachadas para o servidor Apple Push Notification Service (APNs) ou Google Cloud Messaging
(GCM) e, em seguida, enviadas para clientes móveis registrados.

![Visão geral de push](images/overview.jpg)


###Aplicativos Remotos

Na inicialização, os
aplicativos móveis se registram e assinam o Push
                Notification Service para receber notificações.

###Aplicativos backend

Os aplicativos backend podem ser locais ou em uma nuvem pública. Aplicativos backend usam o Push
                        Notification Service para enviar notificações
sensíveis ao contexto para usuários móveis. Os aplicativos backend
não são necessários para manter e gerenciar dispositivos
móveis e informações do usuário para enviar notificações
push. Ao contrário, os aplicativos backend podem usar o
Push Notification Service.

###Proprietário backend do app

A função que criou o aplicativo backend móvel que
empacota uma instância do Push Notification Service. Essa pessoa
configura e instala o Push Notification Service
para adequar os aplicativos corporativos que usam o Push Notification
Service e aplicativos  móveis que são o destino das notificações push.

###Serviço de notificação push

O Serviço de notificação push gerencia todas as informações
relacionadas aos dispositivos que são registradas para obter notificações. O serviço mantém seus aplicativos
transparentes para os detalhes de tecnologia de envio de notificações para essas
plataformas móveis heterogêneas, manipulando tudo isso.

###Gateways

Serviços de nuvem específicos de plataforma do dispositivo
móvel, como Google Cloud
                        Messaging (GCM) ou Apple Push Notification
Service (APNs) usam o Push
                        Notification Service para despachar
notificações para os aplicativos móveis.

## Tipos de notificação push
{: #overview-push-types}

###Difusão

Quando um aplicativo móvel se registra no Serviço de notificação push, ele pode
começar a receber transmissões. Notificações de transmissão são mensagens de
notificação destinadas a todos os dispositivos que têm o aplicativo
instalado e configurado para o Push Notification Service. As notificações de transmissão são
ativadas por padrão com qualquer aplicativo que esteja ativado para
notificações push. Qualquer aplicativo ativado para o Serviço de notificação push tem uma
assinatura predefinida para a tag Push.ALL, que é usada pelo servidor para transmitir
mensagens de notificação a todos os dispositivos. Para enviar uma
notificação de transmissão usando a API Push REST, assegure-se de que
o "destino" seja um JSON vazio ao postar no recurso de mensagens.

###Notificações baseadas em tag

Notificações de identificação são mensagens de notificação destinadas a todos os
dispositivos que assinaram uma identificação específica. As notificações baseadas em identificação
permitem a segmentação de notificações com base em áreas ou tópicos de assunto. Os destinatários da notificação podem optar por receber notificações somente se for
sobre um assunto ou um tópico de interesse. Portanto, a notificação baseada em
identificação fornece um meio de segmentar destinatários. Esse recurso ativa
a capacidade de definir identificações e, em seguida, de enviar e receber mensagens por identificações. Uma
mensagem é destinada somente aos dispositivos que assinaram uma identificação. Deve-se
primeiramente criar as identificações para o aplicativo, configurar as assinaturas da identificação
e, em seguida, iniciar as notificações baseadas em identificação. Para enviar uma notificação baseada em tag usando a API
REST, assegure-se de que os "tagnames" sejam fornecidos ao postar no
recurso de mensagem.

###Notificações unicast

Notificações unicast são mensagens de notificação direcionadas para um dispositivo
específico. As notificações unicast não requerem
configuração adicional e são ativadas por padrão quando o aplicativo está ativado
para notificações push. Para enviar uma notificação unicast que use a API REST,
certifique-se de que os deviceIds sejam fornecidos ao postar em um recurso de mensagem.

###Notificações com base em plataforma

Notificações podem ser
destinada a atingir uma plataforma de dispositivo
específica. Por exemplo, uma notificação pode ser enviada a todos os
usuários do Android somente. Para enviar uma notificação baseada em
plataforma usando a API REST, assegure-se de que as plataformas
destinadas sejam fornecidas ao postar no recurso de mensagem. Especifique as plataformas como uma matriz. As plataformas
suportadas são como a seguir:
* A (Apple)
* G (Google)
