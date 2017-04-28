---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolução de problemas
{: #errors}
Última atualização: 12 de abril de 2017
{: .last-updated}

Este tópico orienta na identificação e resolução dos prováveis cenários de erro que você pode encontrar ao usar o Push Notifications service.

## Resolvendo problemas comuns de notificação push
{: #troubleshooting_notification_errors}

### Ocorreu um erro do servidor interno. Contate o administrador. (Código de erro interno: PUSHD102E)
{: #troubleshooting_notification_internal}

**Explicação**: este erro poderá ocorrer se
você tiver criado uma instância push antes de novembro de 2015.  

**Resposta do usuário**: para resolver esse problema, exclua a instância de push e
crie uma nova. Observe que, ao excluir a instância de push, suas tags não serão preservadas.


### UnauthorizedRegistration
{: #troubleshooting_notification_unauth}

**Explicação**: o Chrome Web Push não
funciona com as Chaves do Firebase Cloud Messaging (FCM). Caso você não possa receber notificações push da web no Chrome após mudar para o FCM do GCM, é porque o website foi configurado anteriormente para
funcionar com o projeto GCM e o novo projeto foi criado no FCM. Os tokens gerados que identificam o navegador são armazenadas em cache pelo navegador Chrome.

**Resposta do usuário**: é possível resolver este problema ao remover os cookies e
reconfigurar as permissões do navegador. Isso
solicitaria permissões para ativar Notificações push. 


### Os trabalhadores de serviço não são suportados neste navegador
{: #troubleshooting_notification_service_workers}

**Explicação**: o SDK que foi incluído como uma parte de `BMSPushSDK.js` usando o trabalhador de serviço não está disponível. 

**Resposta do usuário**: é recomendável alternar para um navegador que suporte o trabalhador de serviço. As versões suportadas dos navegadores são o Firefox versão 49 ou mais recente e o Chrome versão 53 (64 bits) ou mais recente.


### SecurityError: a operação é insegura
{: #troubleshooting_notification_insecure}

**Explicação**: você poder ver o erro ao ativar o console da web no Firefox. O suporte de push da web no serviço de Notificação push requer que o website seja acessado com o protocolo `https`, em vez de `http`.

**Resposta do usuário**: recomenda-se tentar a conexão ao website usando `https` no navegador.


## Resolvendo erros de configuração Push da web
{: #troubleshooting_configuration_errors}

É possível diagnosticar erros relacionados à configuração push da web passando pelo arquivo `BMSPushSDK.js`. O arquivo contém informações sobre a falha. 

Para analisar um erro retornado no retorno de chamada, considere o código de amostra a seguir:

```
function showStatus(response) {
 if(response.statusCode == 200 || response.statusCode == 201) {
   		document.getElementById("status").innerHTML = "Response is " + response.response;
   	}
   	else if(response.statusCode == 0) {
  		if(response.response) {
  			document.getElementById("status").innerHTML = response.response;	
    		}
    		else {
    			document.getElementById("status").innerHTML = "There is a possible CORS or access issue while attempting the request.";	
   		}   		
   	}
   	else {
   		document.getElementById("status").innerHTML = "Response is " + response.response + " with the error " 
		+ response.error + " and the status code " + response.statusCode;
   	}
 	}
```
	{: codeblock}


- Se o `applicationId` estiver configurado incorretamente, a solicitação inicial para o serviço {{site.data.keyword.mobilepushshort}} falhará, por conseguinte o statusCode será configurado como zero (0).
- Um código de status de 200 ou 201 denota uma resposta bem-sucedida.
- No caso de o `clientSecret` ser inválido, uma resposta 401 será configurada no statusCode. O elemento `response.reponse` conterá uma descrição do erro.


## Resolvendo mensagens de erro do Push Notifications service
{: #troubleshooting_service_errors}

As mensagens de erro de {{site.data.keyword.mobilepushshort}} a seguir são retornadas em resposta a solicitações da API REST.

Resposta de erro de amostra:
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"
	}
```
		    {: codeblock}

Para obter informações adicionais sobre um erro, procure nos
docs o código de erro relacionado.

### FPWSE0001E
{: #error_fpwse0001e}

**Explicação**: o recurso que você está tentando consultar, como uma
tag ou assinatura, não está disponível no servidor.

**Resposta do usuário**: crie o recurso que foi relatado na mensagem. Como alternativa, é possível fornecer o identificador
correto para consultar o recurso.


### FPWSE0002E
{: #error_fpwse0002e}

**Explicação**: o recurso que você está tentando criar já está disponível no servidor. O
recurso pode ser uma identificação, uma assinatura, etc.

**Resposta do usuário**: crie o recurso com um identificador diferente.


### FPWSE0003E
{: #error_fpwse0003e}

**Explicação**: a configuração de pré-requisito para o serviço {{site.data.keyword.mobilepushshort}} não foi concluída. É possível
que você esteja tentando obter as credenciais de Apple Push Notification service (APNs) antes de elas serem
configuradas.

**Resposta do usuário**: assegure-se de que o serviço
{{site.data.keyword.mobilepushshort}}
tenha sido configurado com certificados de segurança válidos para APNs. Para obter mais informações, veja [Configurando credenciais para um provedor de notificação ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](t__main_push_config_provider.html){: new_window}.


### FPWSE0004E
{: #error_fpwse0004e}

**Explicação**: o corpo de JSON incluído na solicitação não é válido.


**Resposta do usuário**: assegure-se de usar uma sintaxe válida de JSON na
solicitação.



### FPWSE0005E
{: #error_fpwse0005e}

**Explicação**: a solicitação para o servidor
{{site.data.keyword.mobilepushshort}} está incorreta ou incompleta,
pois o corpo de JSON não contém os valores de propriedade necessários para concluir a solicitação de API. Por exemplo, uma senha não é válida ou
um token de dispositivo  está ausente.


**Resposta do usuário**: revise a mensagem para saber qual valor de propriedade está
ausente ou não é válido e, em seguida, forneça as informações necessárias.



### FPWSE0006E
{: #error_fpwse0006e}

**Explicação**: o corpo de JSON da solicitação possui parâmetros que o servidor
{{site.data.keyword.mobilepushshort}} não entende.


**Resposta do usuário**: verifique se o corpo de JSON na solicitação segue o
formato da solicitação que é esperado pelo servidor {{site.data.keyword.mobilepushshort}}. Para obter mais informações, veja [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0007E 
{: #error_fpwse0007e}

**Explicação**: a URL de solicitação possui uma sequência de consultas com parâmetros
não reconhecidos. Por exemplo, se a solicitação para excluir a assinatura tiver parâmetros diferentes de deviceId e tagName, esse erro poderá ocorrer.


**Resposta do usuário**: verifique se o corpo de JSON na solicitação segue o formato
da solicitação que é esperado pelo servidor {{site.data.keyword.mobilepushshort}}. Para obter mais informações, veja [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0008E
{: #error_fpwse0008e}

**Explicação**: a URL de solicitação possui uma sequência de consultas com parâmetros
ausentes. Por exemplo, os parâmetros deviceId e tagName podem estar ausentes na solicitação para excluir a assinatura.


**Resposta do usuário**: verifique se o corpo de JSON na solicitação segue o formato
da solicitação que é esperado pelo servidor {{site.data.keyword.mobilepushshort}}. Para obter mais informações, veja [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0009E
{: #error_fpwse0009e}

**Explicação**: foi feita uma tentativa para enviar notificações, mas não há
dispositivos registrados com o aplicativo.

**Resposta do usuário**: assegure-se de que os dispositivos tenham sido registrados
com o aplicativo antes de tentar enviar notificações.



### FPWSE0010E
{: #error_fpwse0010e}

**Explicação**: a solicitação enviada para o servidor resultou em uma condição de exceção. Uma das condições a seguir pode ter causado esse erro:

- Um subsistema interno usado por
{{site.data.keyword.mobilepushshort}} não está respondendo.
- A solicitação resultou em uma condição de erro que pode não
ser manipulada por {{site.data.keyword.mobilepushshort}}.
- O serviço {{site.data.keyword.mobilepushshort}}
requer atenção do administrador.

**Resposta do usuário**: tente novamente a solicitação. Se o problema persistir, entre em contato com o suporte de
software IBM.



### FPWSE0011E
{: #error_fpwse0011e}

**Explicação**: a assinatura para a tag já existe no servidor. Por exemplo, ao criar
uma assinatura que já existe.

**Resposta do usuário**: crie a assinatura com um nome de tag exclusivo.



### FPWSE0012E
{: #error_fpwse0012e}

**Explicação**: a assinatura para a tag não existe no servidor. Esse erro ocorre quando uma
solicitação é enviada para recuperar ou excluir uma assinatura que não existe.


**Resposta do usuário**: use o nome de tag e o identificador de dispositivo corretos na
solicitação.



### FPWSE0013E
{: #error_fpwse0013e}

**Explicação**: a carga útil de JSON na solicitação não é válida.


**Resposta do usuário**: assegure-se de que a carga útil de JSON seja válida.


### FPWSE0025E
{: #error_fpwse0025e}

**Explicação**: atualmente o servidor não é capaz de manipular a solicitação.

**Resposta do usuário**: envie novamente a solicitação posteriormente.


### FPWSE1007E 
{: #error_fpwse1007e}

**Explicação**: o serviço {{site.data.keyword.mobilepushshort}} foi
desativado para este aplicativo. O motivo pode ser o faturamento, ou o app pode ter sido desativado pelo
administrador.


**Resposta do usuário**: consulte os tópicos de Resolução de problemas no Bluemix Docs
para verificar o status do serviço, revisar informações de resolução de problemas ou para acessar informações sobre como obter
ajuda.



### FPWSE1079E
{: #error_fpwse1079e}

**Explicação**: o valor de compensação que foi fornecido para a operação de consulta
não é válido.

**Resposta do usuário**: assegure-se de que o valor de compensação seja maior ou
igual a zero.



### FPWSE1080E 
{: #error_fpwse1080e}

**Explicação**: o valor do tamanho que foi fornecido para a operação de consulta
não é válido.

**Resposta do usuário**: assegure-se de que o valor do tamanho seja maior que zero.


