---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ativando notificações baseadas no usuário
{: #user_based_notifications}
Última atualização: 16 de janeiro de 2017
{: .last-updated}

{{site.data.keyword.mobilepushshort}} baseado no ID do usuário destina-se a usuários do app móvel com mensagens customizadas. Com
notificações baseadas no usuário, é possível escolher notificar indivíduos
específicos com base em suas preferências.

## Registrar dispositivo com ID do usuário
Para ativar notificações push destinadas por ID do usuário, assegure-se de registrar
o dispositivo com um campo ID do usuário configurado.     

O ID do usuário pode ser qualquer sequência que o aplicativo forneça para o API de registro de dispositivo. Normalmente, um aplicativo móvel primeiro executará um ciclo de autenticação no qual o usuário do app móvel é autenticado junto a um serviço de autenticação, tal como o [{{site.data.keyword.amafull}} ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html){: new_window}. Na autenticação bem-sucedida, o ID de usuário autenticado então é passado para a API de
registro de dispositivo push. 

## Sincronizando o login e o logout do usuário 

É possível optar por enviar notificações somente se o usuário está conectado. 

Por exemplo, considere um dispositivo compartilhado por membros de uma família ou uma equipe no trabalho e há uma necessidade de abordar usuários específicos. Em
um caso de uso desse tipo, haveria uma sequência de login e logout do usuário. Esse
mecanismo de autenticação permite que o aplicativo rastreie a identidade do usuário
presente do aplicativo. Isso assegura que notificações destinadas a um usuário
específico sempre sejam recebidas por esse usuário somente. Após um login bem-sucedido,
chame a API de registro de dispositivo passando o ID do usuário conectado. Da mesma forma, antes do logout, chame a API de remoção de registro do dispositivo. O
sequenciamento dessas APIs de Push com login e logout irá assegurar que as notificações destinadas a um usuário específico sejam enviadas somente para esse usuário.
