---

Título: ativando Notificações push baseadas no usuário

Palavras-chave: notificações push baseadas no usuário, userId
copyright:
 anos: 2015, 2016

---

# Ativando notificações baseadas no usuário
{: #user_based_notifications}
Última atualização: 16 de agosto de 2016
{: .last-updated}

{{site.data.keyword.mobilepushshort}} baseado no ID do usuário destina-se a usuários do app móvel com mensagens customizadas. As notificações baseadas no usuário podem ajudar a encaixar indivíduos específicos para aproveitar suas preferências e escolhas pessoais.  

## Registrar dispositivo com ID do usuário
Para ativar notificações push destinadas por ID do usuário, assegure-se de registrar o dispositivo com um ID de usuário e também de passar o 'clientSecret' alocado quando os serviços de {{site.data.keyword.mobilepushshort}} são provisionados. O registro de dispositivo falhará sem um 'clientSecret' válido.  

O ID do usuário pode ser qualquer sequência que o aplicativo forneça para o API de registro de dispositivo. Geralmente, um aplicativo móvel executará primeiro um ciclo de autenticação no qual o usuário do app móvel seja autenticado em um serviço de autenticação como o [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Na autenticação bem-sucedida, o ID de usuário autenticado é então passado para a API do Registro de dispositivo push, junto a um 'clientSecret'.  A presença de um 'clientSecret' utiliza apenas a associação autorizada de IDs do usuário a registros de dispositivo móvel.

Mantenha o 'clientSecret' confidencial e nunca codificado permanentemente no app móvel. Há vários padrões de inicialização de aplicativo que podem ser usados para puxar o 'clientSecret' dinamicamente durante o tempo de execução do aplicativo. O diagrama de sequência descreve esse padrão.

![Enable_Push](images/init_client_secret.jpg) 

Também é possível registrar um dispositivo para ser associado a um usuário 'anônimo'. Isso requer o uso de uma variante da API de registro de dispositivo que não requer os argumentos ID do usuário e 'clientSecret'.   

## Sincronizando o login/logout do usuário e ativando notificações push 

É possível optar por enviar notificações somente se o usuário está conectado. 

Por exemplo, se um dispositivo é compartilhado por uma família ou por uma equipe no trabalho e você precisa direcionar usuários específicos na família ou na equipe.  Em um caso de uso desse tipo, haveria uma sequência de login e logout do usuário que guardaria o aplicativo para controlar a identidade do usuário presente do aplicativo. Para assegurar que as notificações destinadas a um usuário específico sejam sempre recebidas somente por esse usuário, após um login bem-sucedido, chame a API de registro de dispositivo passando o ID de usuário do usuário conectado. Da mesma forma, antes do logout, chame a API de remoção de registro do dispositivo. O sequenciamento dessas APIs de Push com login e logout irá assegurar que as notificações push destinadas a um usuário específico sejam enviadas somente para esse usuário.
