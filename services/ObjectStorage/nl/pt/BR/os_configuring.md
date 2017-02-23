---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Configurando a CLI para usar comandos Swift e Cloud Foundry

Para interagir com o serviço {{site.data.keyword.objectstorageshort}} usando comandos Swift ou Cloud Foundry, deve-se instalar o software obrigatório.
{: shortdesc}


## Instalando o cliente Swift {: #install-swift-client}

Caso você ainda tenha feito isso, instale o software obrigatório a seguir.
* Python 2.7 ou mais recente
* Pacote setuptools
* Pacote pip
* CLI do Cloud Foundry


Para instalar o cliente Python Swift, execute o comando a seguir:
```
pip install python-swiftclient
```
{: pre}

Para instalar o cliente Python Keystone, execute o comando a seguir:
```
pip install python-keystoneclient
```
{: pre}

Para obter mais informações sobre os pré-requisitos, consulte <a href="http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software" target="_blank">a
documentação do OpenStack. <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>



## Configurando o Cliente {: #setup-swift-client}

Para configurar o cliente Swift, deve-se `exportar` suas informações sobre autenticação. É possível [gerar credenciais](/docs/services/ObjectStorage/os_credentials.html) por meio da CLI usando comandos Cloud Foundry ou cURL ou por meio da UI do {{site.data.keyword.Bluemix_notm}}. O cliente obtém as informações das variáveis de ambiente na tabela a seguir.

<table>
<caption> Tabela 1. Variáveis de ambiente e descrições </caption>
  <tr>
    <th> Variável de ambiente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> Seu ID do usuário do {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> A senha para a instância do {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> Seu ID do projeto. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> A região na qual seus objetos são armazenados. O
{{site.data.keyword.objectstorageshort}} está disponível nas regiões Dallas e
Londres. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> A URL do terminal. Certifique-se de que <code>/v3</code> esteja incluído no final da URL. </td>
  </tr>
</table>



Para exportar suas informações autenticação, insira suas credenciais e execute o comando a seguir:
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Exemplo:
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

swift auth
```
{: screen}
