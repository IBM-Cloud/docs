---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-16"

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
    <td> O tempo durante o qual a URL provisória estará disponível, expresso em segundos. </td>
  </tr>
  <tr>
    <td> [path] </td>
    <td> O caminho completo do objeto expresso como <code>/v1/<i>auth_account</i>/<i>container_name</i>/<i>object_name</i>.</code> Para obter mais informações, veja a <a href="https://console.bluemix.net/docs/services/ObjectStorage/os_api.html#access-points">{{site.data.keyword.objectstorageshort}} documentação da URL</a>. </td>
  </tr>
  <tr>
    <td> [key] </td>
    <td> A chave secreta configurada na etapa 2. </td>
  </tr>
</table>

Tabela 2: argumentos posicionais da URL provisória

5. (Opcional:) anexe a URL retornada ao nome do seu cluster para obter uma URL completa. É possível então usar a URL completa para fazer download de objetos com
qualquer cliente HTTP compatível, como cURL, wget ou Firefox.
