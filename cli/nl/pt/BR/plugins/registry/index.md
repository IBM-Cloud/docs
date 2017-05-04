---



copyright:

  years: 2017

lastupdated: "2017-03-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

A CLI do {{site.data.keyword.registrylong}} é um plug-in que permite gerenciar seus recursos de registro, como namespaces e imagens, em sua organização.
{: shortdesc}

**Pré-requisitos**
* Antes de executar os comandos de registro, efetue login no {{site.data.keyword.Bluemix_short}}
 com o comando `bx login` para gerar um token de acesso do {{site.data.keyword.Bluemix_short}}
 e autenticar sua sessão.

<table summary="Gerenciar seu registro de contêineres">
<caption>Tabela 1. Comandos para gerenciar o {{site.data.keyword.registryshort}} no {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar o registro</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
Retorna os detalhes sobre o terminal de API de registro com relação ao qual os comandos são executados.

```
bx cr api
```
{: codeblock}


## bx cr info
Exibe o nome e a organização do registro no qual você estiver com login efetuado. 

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Visualiza detalhes sobre uma imagem específica.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go.</dd>
<dt>IMAGE</dt>
<dd>O caminho completo do registro do {{site.data.keyword.Bluemix_short}} para a imagem que deseja inspecionar. Se uma tag não for especificada no caminho da imagem, a imagem identificada como `latest` será inspecionada. É possível inspecionar múltiplas imagens listando cada caminho de registro privado do {{site.data.keyword.Bluemix_short}} no comando com um espaço entre cada caminho.</dd>
</dl>


## bx cr image-list
Visualiza todas as imagens em sua organização do {{site.data.keyword.Bluemix_short}}.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>--no-trunc</dt>
<dd>(Opcional) Não truncar a saída.</dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Exibe um identificador exclusivo para a imagem no formato: 'repository:tag'.</dd>
<dt>--include-ibm</dt>
<dd>(Opcional) Inclui imagens públicas fornecidas pela IBM na saída. Sem essa permissão, somente imagens privadas são listadas.</dd>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go.</dd>
</dl>


## bx cr image-rm
Exclui uma imagem especificada do seu registro.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>IMAGE</dt>
<dd>O caminho completo do registro do {{site.data.keyword.Bluemix_short}} para a imagem que deseja remover. Se uma tag não for especificada no caminho da imagem, a imagem identificada como `latest` será excluída por padrão. É possível excluir múltiplas imagens listando cada caminho de registro privado do {{site.data.keyword.Bluemix_short}} no comando com um espaço entre cada caminho.</dd>
</dl>


## bx cr login
Se o Docker estiver instalado, esse comando executará o comando `docker login` no registro. O comando `docker login` é necessário para poder executar os comandos `docker push` ou `docker pull` para o registro. Esse comando não é necessário para executar outros comandos `bx cr`. Se o Docker não estiver instalado, esse comando retornará uma mensagem de erro.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Inclui um namespace na sua organização do Bluemix. 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parâmetros**
<dl>
<dt>NAMESPACE</dt>
<dd>O namespace que deseja incluir. O namespace deve ser exclusivo em todas as organizações do {{site.data.keyword.Bluemix_short}}.</dd>
</dl>


## bx cr namespace-list
Visualiza todos os namespaces de sua organização do {{site.data.keyword.Bluemix_short}}.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Remove um namespace de sua organização do {{site.data.keyword.Bluemix_short}}. As imagens nesse namespace são excluídas quando o namespace é removido.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parâmetros**
<dl>
<dt>NAMESPACE</dt>
<dd>O namespace que deseja remover. </dd>
</dl>
