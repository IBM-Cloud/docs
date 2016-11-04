---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Pianificazione dell'eliminazione dell'oggetto {: #schedule-object-deletion}
*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}

Puoi pianificare l'eliminazione dei tuoi oggetti. Puoi farlo utilizzando le intestazioni `X-Delete-At` o `X-Delete-After`.
{: shortdesc}

L'intestazione `X-Delete-At` è un numero intero che rappresenta il momento nel quale eliminare l'oggetto. L'intestazione `X-Delete_After` è un numero intero che rappresenta il numero di secondi dopo cui l'oggetto sarà eliminato. Per utilizzare il client swift per pianificare l'esecuzione dell'eliminazione dell'oggetto esegui il seguente comando che meglio soddisfa i tuoi bisogni.

* Per impostare che l'oggetto venga eliminato in una data/ora specifica, utilizza il seguente comando: 
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    Esempio:
    
    Per impostare che l'oggetto venga eliminato il "2016/04/01 08:00:00", dovrai eseguire il seguente comando: 
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* Per impostare che l'oggetto venga eliminato tra un'ora, utilizza il seguente comando:
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    Esempio:
    
    Per impostare che l'oggetto venga eliminato tra un'ora, dovrai eseguire il seguente comando: 
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* Per rimuovere la data/ora di scadenza dal tuo oggetto, utilizza il seguente comando:
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

Per utilizzare i comandi cURL l'eliminazione dell'oggetto pianificata puoi eseguire il seguente comando che meglio soddisfa i tuoi bisogni. Gli standard dell'ora sono gli stessi del client Swift.

* Per impostare che l'oggetto venga eliminato il "2016/04/01 08:00:00", utilizza il seguente comando:
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
    ```
    {: pre}
    
* Per impostare che l'oggetto venga eliminato tra un'ora, utilizza il seguente comando:
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* Per controllare se l'oggetto ha un'intestazione, utilizza il seguente comando:
    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* Per rimuovere la data/ora di scadenza, utilizza il seguente comando:
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

**Nota:** l'eliminazione effettiva di un oggetto potrebbe non verificarsi nell'esatto momento indicato. Tuttavia, l'oggetto scadrà nel momento specificato. Il che significa che non sarà più raggiungibile. L'eliminazione effettiva avrà luogo la volta successiva in cui viene eseguito il daemon swift-object-expirer configurato nel tuo cluster Swift. 
