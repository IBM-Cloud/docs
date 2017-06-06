---



copyright:

  years: 2017

lastupdated: "2017-05-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

O {{site.data.keyword.registrylong}} CLI é um plug-in para gerenciar seu registro e seus recursos para sua conta.
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
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list (imagens bx cr)](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list (namespaces bx cr)](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr token-add](#bx-cr-token-add)</td>
 </tr>
 <tr>
 <td>[bx cr token-get](#bx-cr-token-get)</td>
 <td>[bx cr token-list (tokens bx cr)](#bx-cr-token-list)</td>
 <td>[bx cr token-rm](#bx-cr-token-rm)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Retorna os detalhes sobre o terminal de API de registro com relação ao qual os comandos são executados.

```
bx cr api
```
{: codeblock}


## bx cr info
Exibe o nome e a conta do registro ao qual você está conectado.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Exibe detalhes sobre uma imagem específica.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parâmetros**


<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go. 


</dd>
<dt>IMAGE</dt>
<dd>O caminho de registro completo do {{site.data.keyword.Bluemix_short}} para a imagem que você deseja inspecionar, que está no formato `namespace/image:tag`. Se uma tag não for especificada no caminho da imagem, a imagem identificada como `latest` será inspecionada. É possível inspecionar múltiplas imagens listando cada caminho de registro privado do {{site.data.keyword.Bluemix_short}} no comando com um espaço entre cada caminho.</dd>
</dl>


## bx cr image-list (imagens bx cr)
Exibe todas as imagens na conta do {{site.data.keyword.Bluemix_short}}.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>--no-trunc</dt>
<dd>(Opcional) Não truncar as compilações de imagem.</dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Cada imagem é listada no formato: `repository:tag`.</dd>
<dt>--include-ibm</dt>
<dd>(Opcional) Inclui imagens públicas fornecidas pela IBM na saída. Sem essa opção, somente imagens privadas serão listadas, por padrão.</dd>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go. 


</dd>

</dl>


## bx cr image-rm
Exclui uma ou mais imagens especificadas do seu registro.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>IMAGE</dt>
<dd>O caminho de registro completo do {{site.data.keyword.Bluemix_short}} para a imagem que você deseja remover, no formato `namespace/image:tag`. Se uma tag não for especificada no caminho da imagem, a imagem identificada como `latest` será excluída por padrão. É possível excluir múltiplas imagens listando cada caminho de registro privado do {{site.data.keyword.Bluemix_short}} no comando com um espaço entre cada caminho.</dd>
</dl>


## bx cr login
Esse comando executa o comando `docker login` no registro. O comando `docker login` é necessário para poder executar os comandos `docker push` ou `docker pull` para o registro. Esse comando não é necessário para executar outros comandos `bx cr`. Se o Docker não estiver instalado, esse comando retornará uma mensagem de erro.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Inclui um namespace em sua conta do {{site.data.keyword.Bluemix_short}}.

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parâmetros**
<dl>
<dt>NAMESPACE</dt>
<dd>O namespace que deseja incluir. O namespace deve ser exclusivo em todas as contas do {{site.data.keyword.Bluemix_short}} na mesma região.</dd>
</dl>


## bx cr namespace-list (namespaces bx cr)
Exibe todos os namespaces pertencentes à sua conta do {{site.data.keyword.Bluemix_short}}.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Remove um namespace de sua conta do {{site.data.keyword.Bluemix_short}}. As imagens nesse namespace são excluídas quando o namespace é removido.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parâmetros**
<dl>
<dt>NAMESPACE</dt>
<dd>O namespace que deseja remover.</dd>
</dl>


## bx cr token-add
Inclui um token que pode ser usado para controlar o acesso a um registro.

```
bx cr token-add [--description VALUE] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Parâmetros**
<dl>
<dt>--description VALUE</dt>
<dd>(Opcional) Especifica o valor como uma descrição para o token, que é exibida quando você executa `bx cr token-list`. Se o seu token for criado automaticamente pelo IBM Bluemix Container Service, a descrição será configurada para seu nome do Cluster do Kubernetes. Nesse caso, o token é removido automaticamente quando o cluster é removido.</dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Exibe o token somente, sem nenhum texto circundante.</dd>
<dt>--non-expiring</dt>
<dd>(Opcional) Cria um token com acesso que não expira. Sem esse conjunto de parâmetros, o acesso por meio de um token expirará após 24 horas, por padrão.</dd>
<dt>--readwrite</dt>
<dd>(Opcional) Cria um token que concede acesso de leitura e gravação. Sem essa opção, o acesso será somente leitura, por padrão.</dd>
</dl>


## bx cr token-get
Recuperar o token especificado do registro.

```
bx cr token-get TOKEN
```

{: codeblock}

**Parâmetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) O identificador exclusivo do token que você deseja recuperar.</dd>
</dl>


## bx cr token-list (tokens bx cr)
Exibe todos os tokens que existem para sua conta do {{site.data.keyword.Bluemix_short}}.

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Parâmetros**
<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formata os elementos de saída usando um modelo Go. 


</dd>
</dl>


## bx cr token-rm
Remover um ou mais tokens especificados.

```
bx cr token-rm TOKEN [TOKEN]
```
{: codeblock}

**Parâmetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) TOKEN pode ser o próprio token ou o identificador exclusivo do token, conforme mostrado em `bx cr token-list`. É possível especificar múltiplos tokens e devem ser separados por um espaço.</dd>
</dl>


</dd>
</dl>


