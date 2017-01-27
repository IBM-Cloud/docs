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


# Tipos de acesso

Usuários do {{site.data.keyword.objectstorageshort}} podem ser administrativos ou não
administrativos. As listas de controle de acesso são ativadas por usuários administradores no nível de contêiner.
{: shortdesc}

<table>
<caption> Tabela 1. Funções de usuário definidas</caption>
  <tr>
    <th> Usuários administrativos (administradores) </th>
    <th> Usuários não administrativos (membros) </th>
  </tr>
  <tr>
    <td> Gerenciar controle de acesso </td>
    <td> Por padrão, sem acesso ao serviço ou aos seus contêineres </td>
  </tr>
  <tr>
    <td> Podem criar e excluir contêineres </td>
    <td> Podem executar ações com base nas ACLs de leitura/gravação de contêineres </td>
  </tr>
  <tr>
    <td> Podem ler e gravar em contêineres </td>
    <td> Podem executar ações conforme determinado pelo administrador </td>
  </tr>
</table>


É possível gerenciar usuários do {{site.data.keyword.objectstorageshort}} por meio da interface com o usuário do {{site.data.keyword.Bluemix_notm}}, da API do Cloud Foundry ou da CLI do
Cloud Foundry.
