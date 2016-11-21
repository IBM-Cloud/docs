---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Planejando a exclusão de objeto {: #schedule-object-deletion}
*Última atualização: 19 de outubro de 2016*
{: .last-updated}

É possível planejar a exclusão de seus objetos. Isso pode ser feito usando um dos dois cabeçalhos `X-Delete-At` ou `X-Delete-After`.
{: shortdesc}

O cabeçalho `X-Delete-At` usa um número inteiro que representa o período no qual excluir o objeto. O cabeçalho `X-Delete_After` usa um número inteiro que representa o número de segundos após os quais o objeto será excluído. Para
usar o cliente swift para planejar a exclusão de objeto, execute o comando a seguir que
melhor se ajuste à sua necessidade.

* Para configurar o objeto a ser excluído em uma data e hora específicas, execute o comando a seguir:
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    Exemplo:
    
    Para configurar o objeto a ser excluído em "2016/04/01 08:00:00", você executaria o comando a seguir:
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* Para configurar o objeto a ser excluído em uma hora, use o comando a seguir:
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    Exemplo:
    
    Para configurar o objeto a ser excluído daqui a uma hora, você executaria o comando a seguir:
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* Para remover o prazo de expiração do objeto, use o comando a seguir:
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

Para usar comandos cURL para exclusão de objeto planejado, é possível executar o
comando a seguir que melhor se ajuste à sua necessidade. Os padrões para horário são os
mesmos do cliente Swift.

* Para configurar o objeto a ser excluído em "01/04/2016 8h", use o comando a seguir:
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
    ```
    {: pre}
    
* Para configurar o objeto a ser excluído em uma hora, use o comando a seguir:
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* Para verificar se o objeto tem o cabeçalho, use o comando a seguir:
    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* Para remover o prazo de expiração, use o comando a seguir:
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

**Nota:** a exclusão real de um objeto pode não acontecer no horário exato indicado. No entanto, o objeto irá de fato expirar no horário especificado. Isso significa que não será mais acessível. A exclusão real ocorrerá na próxima vez que o daemon swift-object-expirer configurado no cluster Swift for executado.
