---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Trabalhando com versão de objetos {: #work-with-object-versioning}

*Última atualização: 19 de outubro de 2016*
{: .last-updated}

Com a versão de objeto, você pode manter versões separadas de seus objetos sem
renomear seus arquivos. Isso permite ver um histórico de cada objeto e controlar quando
as mudanças foram feitas.
{: shortdesc}


### Configurando versão de objeto{: #setting-up-versioning}

É possível configurar versões de cada objeto em seu contêiner usando o parâmetro `X-Versions-Location`. Para isso, crie um contêiner adicional para manter as versões mais antigas de seus objetos como a seguir.

É possível configurar a versão de objeto por meio do cliente Swift ou usando comandos cURL.
* Se você estiver usando o cliente Swift, execute o comando a seguir:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* Se você estiver usando o cURL, poderá configurá-lo desta forma:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**Nota**: os objetos em seu contêiner de backup serão
automaticamente denominados com o formato a seguir: `<Length><Object_name>/<Timestamp>`.
<table>
  <tr>
    <th> Atributo </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> O comprimento do nome de seu objeto. Este é um número hexadecimal de 3 caracteres preenchido com zero.</td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> O nome do objeto. </td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> O registro de data e hora de quando essa versão do objeto foi originalmente transferida por upload.</td>
  </tr>
</table>

### Desativando versão de objeto{: #disabling-versioning}

É possível desativar a versão por meio do cliente Swift ou usando comandos cURL.

* Para usar o cliente Swift, execute o comando a seguir:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* Execute o comando cURL a seguir para desativar a versão:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### Tutorial de versão de objeto {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

É possível usar o tutorial a seguir para entender o ciclo de vida integral de
versão de objeto.

1. Crie um contêiner chamado `container_one`.

    ```
    swift post container_one
    ```
    {: pre}
    
3. Crie um segundo contêiner com o nome `container_two`.

    ```
    swift post container_two
    ```
    {: pre}
    
2. Configure a versão.

    ```
    swift post container_one -H "X-Versions-Location:container_two"
    ```
    {: pre}
    
4. Faça upload de um objeto para seu contêiner principal pela primeira vez.

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. Faça upload de uma nova versão do objeto para container_one. Ao fazer upload de
uma nova versão de seu arquivo, a versão anterior é automaticamente movida para o
contêiner de backup especificado ao configurar a versão.

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. Para ver a nova versão de seu arquivo no contêiner, liste os objetos em container_one.

    ```
    swift list container_one
    ```
    {: pre}
    
9. Liste os objetos em container_two. Você verá que a versão anterior de seu
arquivo estará armazenada nesse contêiner.

    ```
    swift list container_two
    ```
    {: pre}
    
10. Exclua o objeto em container_one. Quando você excluir o objeto, a versão
anterior em seu contêiner de backup será automaticamente movida para o contêiner
principal.

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. Liste ambos os contêineres. Você verá que seu arquivo original em
`container_one` e `container_two` estará vazio.

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
