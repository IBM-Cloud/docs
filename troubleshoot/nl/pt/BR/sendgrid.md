{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# Resolução de problemas de SendGrid
{: #ts_sendgrid}

*Última atualização: 9 de dezembro de 2015*

Aqui está a resposta para uma pergunta sobre como usar o SendGrid no {{site.data.keyword.Bluemix}}.
{:shortdesc}


## Impossível enviar e-mails usando SendGrid
{: #ts_sendgrid_email}

Se não conseguir enviar e-mails usando o serviço SendGrid, você talvez tenha atingido o limite de e-mails permitido por instância de serviço.
{:shortdesc}


Depois que você tiver enviado o número máximo de e-mails que são permitidos, não é possível usar o serviço SendGrid para enviar mais e-mails.
{: tsSymptoms}


Ao enviar e-mails usando o serviço SendGrid, você é limitado a enviar 25.000 e-mails por instância de serviço por mês. Depois que você tiver atingido o limite, o SendGrid para de enviar e-mails e encargos adicionais não são incorridos para usar esse serviço.
{: tsCauses}

Para verificar o número restante de e-mails que são permitidos, clique na instância de serviço SendGrid a partir do painel do {{site.data.keyword.Bluemix_notm}} e, em seguida, clique em **ABRIR PAINEL DO SENDGRID**. É possível
ver o número no campo **Créditos restantes**.


Se desejar enviar mais e-mails depois de atingir o limite de
25.000 e-mails por instância de serviço por mês, será possível incluir uma outra
instância de serviço. Para obter mais informações sobre SendGrid, veja [Introdução ao SendGrid](https://sendgrid.com/docs/index.html){: new_window}.    
{: tsResolve}

