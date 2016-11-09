---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Criando uma URL provisória {: #create-temporary-url}

*Última atualização: 19 de outubro de 2016*
{: .last-updated}

Uma URL provisória é uma URL longa, difícil de adivinhar que pode ser usada por um período especificado para fazer download de objetos sem requerer autenticação adicional.
{: shortdesc}


1. Identifique suas informações de autenticação imprimindo os dados da sua conta com o comando a seguir:

    ```
    swift stat
    ```
    {: pre}
    
    **Nota**: localize o campo Conta e anote a sequência integral por trás de *Conta*: incluindo `AUTH_`.
2. Configure uma chave secreta. Essa chave pode ser qualquer coisa que você selecionar, mas a melhor prática é selecionar uma sequência longa, aleatória e difícil de adivinhar. Para
configurar a chave, execute o comando a seguir:

    ```
    swift post -m "Temp-URL-Key:<key>"
    ```
    {: pre}
    
3. Verifique se `Temp-URL-Key` foi configurado com êxito executando o comando a seguir.

    ```
    swift stat
    ```
    {: pre}
    
4. Crie uma URL provisória executando o comando a seguir:

    ```
    swift tempurl GET <seconds> <path> <key>
    ```
    {: pre}
    
    A tabela a seguir explica os argumentos posicionais que o comando Swift `tempurl` executa.
    <table>
      <tr>
        <th> Argumento </th>
        <th> Descrição </th>
      </tr>
      <tr>
        <td> [method] </td>
        <td> GET para permitir download. PUT para permitir upload. </td>
      </tr>
      <tr>
        <td> [segundos] </td>
        <td> Tempo, em segundos, em que a URL provisória estará disponível. </td>
      </tr>
      <tr>
        <td> [path] </td>
        <td> O caminho completo do objeto expresso como `/v1/<auth_account>/<container_name>/<object_name>`. Para obter mais informações, consulte a [documentação da URL do {{site.data.keyword.objectstorageshort}}](/os_api.html#access-points). </td>
      </tr>
      <tr>
        <td> [key] </td>
        <td> A chave secreta que você configura na etapa 2. </td>
      </tr>
    </table>
    *Tabela 2: argumentos posicionais tempurl*
5. (*Opcional*): Anexe a URL retornada ao nome do cluster para obter
uma URL completa. É possível então usar a URL completa para fazer download de objetos com
qualquer cliente HTTP compatível, como cURL, wget ou Firefox.
