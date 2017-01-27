---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Excluindo objetos

Depois que você não tiver mais necessidade deles, será possível excluir os objetos e os contêineres de sua instância de armazenamento. É possível executar a exclusão manualmente ou [planejar um horário](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion) para os objetos expirarem.
{: shortdesc}

**Nota**: se você excluir seu contêiner, quaisquer objetos armazenados nesse contêiner serão excluídos.


## Excluindo objetos e contêineres por meio da UI {: #deleting-ui}

1. No painel da instância de serviço, selecione o contêiner com o arquivo que não é mais necessário.
2. Selecione **Excluir arquivo** no menu suspenso **Ações**.
3. Se você não tiver mais uso para seu contêiner, selecione **Excluir contêiner** no menu suspenso **Ações**.



## Excluindo objetos e contêineres por meio da CLI {: #deleting-cli}

1.  Se você não tiver efetuado login no {{site.data.keyword.Bluemix_notm}}, efetue login na organização e no espaço que contêm sua instância do {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Opcional: confirme se você tem um backup de seus objetos antes de excluir os arquivos e contêineres.

3. Execute o comando a seguir para excluir um arquivo:
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

4. Para excluir seu contêiner, execute o comando a seguir:
  ```
  swift delete <container_name>
  ```
  {: pre}



## Planejando a exclusão de objeto {: #schedule-object-deletion}


É possível planejar a exclusão de seus objetos usando os cabeçalhos `X-Delete-At` ou `X-Delete-After`.
{: shortdesc}

O cabeçalho `X-Delete-At` usa um número inteiro que representa o período de tempo no qual excluir o objeto. O cabeçalho `X-Delete_After` usa um número inteiro que representa o número de segundos após os quais o objeto é excluído.

**Nota:** a exclusão real de um objeto pode não acontecer no horário exato indicado. No entanto, o objeto irá de fato expirar no horário especificado. Nesse momento, o objeto ainda estará acessível. A exclusão real ocorrerá na próxima vez que o daemon swift-object-expirer, que está configurado em seu cluster Swift, for executado.

#### Para usar comandos Swift:

* Para configurar o objeto a ser excluído em uma data e hora específicas, execute o comando a seguir:

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    Exemplo:
    para configurar o objeto a ser excluído em "01/04/2016 08h", você executaria o comando a seguir:

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* Para configurar o objeto a ser excluído após uma quantia específica de tempo, use o comando a seguir:

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    Exemplo:
    para configurar o objeto a ser excluído daqui a uma hora, você executaria o comando a seguir:

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* Para remover o prazo de expiração do objeto, use o comando a seguir:

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### Para usar comandos cURL:

* Para configurar o objeto a ser excluído em "01/04/2016 8h", use o comando a seguir:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
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
