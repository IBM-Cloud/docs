---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mensagens de erro
de serviço {{site.data.keyword.mobilepushshort}}
{: #errors}
Última atualização: 16 de janeiro de 2017
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

**Explicação**: o recurso que você está tentando consultar, como uma
tag ou assinatura, não está disponível no servidor.

**Resposta do usuário**: crie o recurso que foi relatado na mensagem. Como alternativa, é possível fornecer o identificador
correto para consultar o recurso.


## FPWSE0002E
{: #error_fpwse0002e}

**Explicação**: o recurso que você está tentando criar já está disponível no servidor. O
recurso pode ser uma identificação, uma assinatura, etc.

**Resposta do usuário**: crie o recurso com um identificador diferente.


## FPWSE0003E
{: #error_fpwse0003e}

**Explicação**: a configuração de pré-requisito para o serviço {{site.data.keyword.mobilepushshort}} não foi concluída. É possível
que você esteja tentando obter as credenciais de Apple Push Notification service (APNs) antes de elas serem
configuradas.

**Resposta do usuário**: assegure-se de que o serviço
{{site.data.keyword.mobilepushshort}}
tenha sido configurado com certificados de segurança válidos para APNs. Para obter mais informações, veja [Configurando credenciais para APNs ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](t_push_provider_ios.html "Ícone de link externo"){: new_window}.


## FPWSE0004E
{: #error_fpwse0004e}

**Explicação**: o corpo de JSON incluído na solicitação não é válido.


**Resposta do usuário**: assegure-se de usar uma sintaxe válida de JSON na
solicitação.



## FPWSE0005E
{: #error_fpwse0005e}

**Explicação**: a solicitação para o servidor
{{site.data.keyword.mobilepushshort}} está incorreta ou incompleta,
pois o corpo de JSON não contém os valores de propriedade necessários para concluir a solicitação de API. Por exemplo, uma senha não é válida ou
um token de dispositivo  está ausente.


**Resposta do usuário**: revise a mensagem para saber qual valor de propriedade está
ausente ou não é válido e, em seguida, forneça as informações necessárias.



## FPWSE0006E
{: #error_fpwse0006e}

**Explicação**: o corpo de JSON da solicitação possui parâmetros que o servidor
{{site.data.keyword.mobilepushshort}} não entende.


**Resposta do usuário**: verifique se o corpo de JSON na solicitação segue o
formato da solicitação que é esperado pelo servidor {{site.data.keyword.mobilepushshort}}. Para obter mais informações, veja [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile.{DomainName}/imfpush/ "Ícone de link externo"){: new_window}.



## FPWSE0007E 
{: #error_fpwse0007e}

**Explicação**: a URL de solicitação possui uma sequência de consultas com parâmetros
não reconhecidos. Por exemplo, se a solicitação para excluir a assinatura tiver parâmetros diferentes de deviceId e tagName, esse erro poderá ocorrer.


**Resposta do usuário**: verifique se o corpo de JSON na solicitação segue o formato
da solicitação que é esperado pelo servidor {{site.data.keyword.mobilepushshort}}. Para obter mais informações, veja [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile.{DomainName}/imfpush/ "Ícone de link externo"){: new_window}.



## FPWSE0008E
{: #error_fpwse0008e}

**Explicação**: a URL de solicitação possui uma sequência de consultas com parâmetros
ausentes. Por exemplo, os parâmetros deviceId e tagName podem estar ausentes na solicitação para excluir a assinatura.


**Resposta do usuário**: verifique se o corpo de JSON na solicitação segue o formato
da solicitação que é esperado pelo servidor {{site.data.keyword.mobilepushshort}}. Para obter mais informações, veja [APIs de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile.{DomainName}/imfpush/ "Ícone de link externo"){: new_window}.



## FPWSE0009E
{: #error_fpwse0009e}

**Explicação**: foi feita uma tentativa para enviar notificações, mas não há
dispositivos registrados com o aplicativo.

**Resposta do usuário**: assegure-se de que os dispositivos tenham sido registrados
com o aplicativo antes de tentar enviar notificações.



## FPWSE0010E
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



## FPWSE0011E
{: #error_fpwse0011e}

**Explicação**: a assinatura para a tag já existe no servidor. Por exemplo, ao criar
uma assinatura que já existe.

**Resposta do usuário**: crie a assinatura com um nome de tag exclusivo.



## FPWSE0012E
{: #error_fpwse0012e}

**Explicação**: a assinatura para a tag não existe no servidor. Esse erro ocorre quando uma
solicitação é enviada para recuperar ou excluir uma assinatura que não existe.


**Resposta do usuário**: use o nome de tag e o identificador de dispositivo corretos na
solicitação.



## FPWSE0013E
{: #error_fpwse0013e}

**Explicação**: a carga útil de JSON na solicitação não é válida.


**Resposta do usuário**: assegure-se de que a carga útil de JSON seja válida.



## FPWSE1007E 
{: #error_fpwse1007e}

**Explicação**: o serviço {{site.data.keyword.mobilepushshort}} foi
desativado para este aplicativo. O motivo pode ser o faturamento, ou o app pode ter sido desativado pelo
administrador.


**Resposta do usuário**: consulte os tópicos de Resolução de problemas no Bluemix Docs
para verificar o status do serviço, revisar informações de resolução de problemas ou para acessar informações sobre como obter
ajuda.



## FPWSE1079E
{: #error_fpwse1079e}

**Explicação**: o valor de compensação que foi fornecido para a operação de consulta
não é válido.

**Resposta do usuário**: assegure-se de que o valor de compensação seja maior ou
igual a zero.



## FPWSE1080E 
{: #error_fpwse1080e}

**Explicação**: o valor do tamanho que foi fornecido para a operação de consulta
não é válido.

**Resposta do usuário**: assegure-se de que o valor do tamanho seja maior que zero.



