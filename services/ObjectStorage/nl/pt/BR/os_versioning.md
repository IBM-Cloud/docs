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


# Configurando versão de objeto {: #setting-up-versioning}

É possível manter versões antigas de seus objetos automaticamente configurando a versão do objeto. Com a versão, é possível ver um histórico de cada objeto.
{: shortdesc}

Ao fazer upload de uma nova versão de seu arquivo para o contêiner principal, a versão
anterior será movida automaticamente para o contêiner de backup. Se você excluir o arquivo do seu contêiner principal, a versão mais recente será movida automaticamente do contêiner de backup para o contêiner principal para substituir o arquivo excluído.

1. Crie um contêiner e forneça um nome a ele. Substitua a variável *container_name* pelo nome que você deseja fornecer ao contêiner.

    ```
    swift post <container_name>
    ```
    {: pre}

2. Crie um segundo contêiner para agir como armazenamento de backup e forneça um nome a ele.

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. Configure a versão.

    Comando Swift:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. Faça upload de um objeto para seu contêiner principal pela primeira vez.

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. Faça uma mudança em seu objeto.

6. Faça upload da nova versão do objeto para seu contêiner principal.

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  Os objetos no contêiner de backup são nomeados automaticamente com o formato a seguir: `<Length><Object_name>/<Timestamp>`.
  <table>
  <caption> Tabela 1. Atributos de nomenclatura descritos</caption>
    <tr>
      <th> Atributo </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i>Length</i> </td>
      <td> O comprimento do nome de seu objeto. Este é um número hexadecimal de 3 caracteres preenchido com zero. </td>
    </tr>
    <tr>
      <td> <i>Object_name</i> </td>
      <td> O nome do objeto. </td>
    </tr>
    <tr>
      <td> <i>Timestamp</i> </td>
      <td> O registro de data e hora de quando essa versão do objeto foi originalmente transferida por upload. </td>
    </tr>
  </table>


6. Liste os objetos em seu contêiner principal para ver a nova versão de seu arquivo.

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. Liste os objetos no contêiner de backup. Você vê a versão anterior de seu arquivo que está armazenada nesse contêiner. Observe que um registro de data e hora está incluído em seu arquivo.

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. Exclua o objeto em seu contêiner principal. Quando você excluir o objeto, a versão
mais recente no contêiner de backup será movida automaticamente de volta para o contêiner principal.

    ```
    swift delete <container_name> <object>
    ```
    {: pre}

9. Opcional: desative a versão de objeto.

    Comando Swift:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    Comando cURL:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
