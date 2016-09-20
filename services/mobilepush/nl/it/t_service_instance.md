---

copyright:
 years: 2015, 2016

---

# Creazione di un'istanza del servizio push
{: #create-push-instance}

Per iniziare a lavorare con {{site.data.keyword.IBM}} {{site.data.keyword.mobilepushshort}}, crea innanzitutto un'applicazione {{site.data.keyword.Bluemix}}; ad esempio un'applicazione Node.js. Crea quindi un'istanza di un servizio push, {{site.data.keyword.mobilepushfull}}, che deve essere associata a questa applicazione Bluemix. Puoi anche eseguire questa operazione andando alla sezione Contenitore tipo del catalogo Bluemix e facendo clic su MobileFirst Services Starter.

**Nota**: se hai configurato le organizzazioni per gestire il tuo ambiente, seleziona l'organizzazione in cui vuoi creare il runtime e i servizi per la tua applicazione mobile.


1. Se non hai un'applicazione Bluemix, devi crearne una, ad esempio un'applicazione Node.js. Per creare un'applicazione Bluemix, bai al Dashboard Bluemix e fai clic su **Crea applicazione**.
	
	**Nota**: se hai un'applicazione, vai al passo 7 per aggiungere un servizio.![Crea un'istanza del servizio](images/create_service_instance1.jpg "Crea un'istanza del servizio")

1. Da **Scegli il template della tua applicazione**, fai clic su **WEB**

3. Nell'area **Scegli il punto di partenza**, seleziona **SDK for Node.js** e quindi fai clic su **CONTINUA**.![Punto di partenza](images/create_service_nodejs2.jpg) 

4. Dal menu a discesa **Spazio**, seleziona il tuo spazio dell'organizzazione.

	![
Select organization space](images/create_a_service3.jpg)
1. In **Nome**, immetti il nome della tua applicazione e, nell'host, immetti il nome dell'host.

1. Dal menu a discesa **Piano selezionato**,
                                        seleziona un piano e fai quindi clic sul pulsante **CREA**. Attendi la preparazione dell'applicazione.

1. Fai clic sul link **Panoramica**.![Aggiungi un servizio](images/create_service_add4.jpg)
1. Fai clic su **Aggiungi un servizio** . Viene visualizzata la schermata CATALOGO.

1. Seleziona **IBM Push Notifications:** e dal menu a discesa **Spazio**, seleziona la tua organizzazione.

	![Menu a discesa dello spazio dell'organizzazione](images/create_service_org.jpg)
1. Nel nome **Servizio**, immetti il nome del servizio Notifica di push.

1. Nel campo **Piano selezionato**, seleziona un piano e fai clic sul pulsante **CREA**.

1. Fai clic su **Sì** per ripreparare l'applicazione.

	![IBM Push Notification Service](images/create_service_notification5.jpg)

1. Fai clic su **Push Notifications** per visualizzare il dashboard Push Notification.
