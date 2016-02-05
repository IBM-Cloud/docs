{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# Traitement des incidents liés à SendGrid
{: #ts_sendgrid}

*Dernière mise à jour : 9 décembre 2015*

Voici la réponse à une question concernant l'utilisation de SendGrid dans {{site.data.keyword.Bluemix}}.
{:shortdesc}


## Impossible d'envoyer des courriers électroniques avec SendGrid
{: #ts_sendgrid_email}

Si vous ne parvenez pas à envoyer des courriers électroniques avec le service SendGrid, il se peut que vous ayez atteint le nombre maximal de
courriers
électroniques pouvant être envoyés par instance de service.
{:shortdesc}


Une fois que vous avez envoyé le nombre maximal de courriers électroniques autorisé, vous ne pouvez plus utiliser le service SendGrid pour envoyer
d'autres
courriers électroniques.
{: tsSymptoms}


Lorsque vous envoyez des courriers électroniques avec le service SendGrid, vous ne pouvez pas envoyer plus de 25000 courriers électroniques par
instance de
service tous les mois. Une fois la limite atteinte, SendGrid arrête d'envoyer des courriers électroniques, et vous n'êtes pas facturé si vous continuez
d'utiliser
ce service.
{: tsCauses}

Pour connaître le nombre restant de courriers électroniques pouvant être envoyés, cliquez sur votre instance de service SendGrid dans le tableau de
bord {{site.data.keyword.Bluemix_notm}}, puis cliquez sur **OPEN SENDGRID DASHBOARD**. Vous
pouvez consulter le nombre dans la zone **Credits Remaining**.


Si vous souhaitez envoyer d'autres courriers électroniques une fois la limite mensuelle de
25000 courriers électroniques par instance de service atteinte, vous pouvez ajouter une autre instance de service. Pour plus d'informations sur SendGrid,
voir [Getting Started with SendGrid](https://sendgrid.com/docs/index.html){: new_window}.    
{: tsResolve}

