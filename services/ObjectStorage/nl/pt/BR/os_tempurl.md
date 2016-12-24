---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Criando uma URL provisória {: #create-temporary-url}

Uma URL provisória é uma URL longa, difícil de adivinhar que pode ser usada por um período especificado para fazer download de objetos sem requerer autenticação adicional.
{: shortdesc}


1. Identifique suas informações de autenticação imprimindo os dados da sua conta com o comando a seguir:

  ```
  swift stat
  ```
  {: pre}
  **Nota**: tome nota da sequência integral atrás de *Conta*, incluindo `AUTH_`.

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
      <td> <i> method </i> </td>
      <td> GET para permitir download. PUT para permitir upload. </td>
    </tr>
    <tr>
      <td> <i> seconds </i> </td>
      <td> O tempo durante o qual a URL provisória está disponível, expresso em segundos. </td>
    </tr>
    <tr>
      <td> <i>path</i> </td>
      <td> O caminho completo do objeto expresso como <code>/v1/<i>auth_account</i>/<i>container_name</i>/<i>object_name</i></code>.</td>
    </tr>
    <tr>
      <td> <i> key </i> </td>
      <td> A chave secreta que você configura na etapa 2. </td>
    </tr>
  </table>

  Tabela 1: Argumentos posicionais da URL provisória

5. Opcional: anexe a URL retornada ao nome do cluster para obter uma URL completa. É possível então usar a URL completa para fazer download de objetos com
qualquer cliente HTTP compatível, como cURL, wget ou Firefox.
