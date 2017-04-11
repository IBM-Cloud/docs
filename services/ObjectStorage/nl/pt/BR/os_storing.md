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

# Armazenando objetos

É possível fazer upload de objetos para o armazenamento usando a UI ou a CLI. O upload de objetos é limitado a um tamanho máximo de 5 GB em um único upload. No entanto, é possível fazer upload de objetos maiores segmentando-os em objetos menores.
{: shortdesc}


## Armazenando objetos em contêineres por meio da UI {: #storing-ui}

**Nota**: quando você faz upload de um arquivo com o mesmo
nome, o {{site.data.keyword.objectstorageshort}} substitui o arquivo armazenado
pelo novo arquivo. Se você fizer download de um arquivo e fizer edições, certifique-se de
dar ao arquivo outro nome ou de
[configurar
a versão do objeto](/docs/services/ObjectStorage/os_versioning.html) antes de fazer upload para manter as duas versões do arquivo.


1. No seu painel de instância de serviço, inclua um contêiner do menu suspenso **Ações**.
2. Nomeie o contêiner e clique em **CRIAR**.
3. No menu suspenso **Ações**, selecione **Incluir arquivos**. Uma
caixa de diálogo é aberta.
4. Selecione o arquivo ou arquivos dos quais você deseja fazer upload e clique em **Abrir**.



## Armazenando objetos em contêineres por meio da CLI {: #storing-cli}

1. Se você não tiver efetuado login no {{site.data.keyword.Bluemix_notm}}, efetue login na organização e no espaço que contêm sua instância do {{site.data.keyword.objectstorageshort}}.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Crie um contêiner do {{site.data.keyword.objectstorageshort}} executando o comando a seguir. A variável *container_name* é agora configurada por você.

  ```
  swift post <container_name>
  ```
  {: pre}

  **Observação**: se você receber uma mensagem de erro, confirme que o [software obrigatório](/docs/services/ObjectStorage/os_configuring.html#install-swift-client) está instalado.

3. Opcional: para verificar se o contêiner foi criado, execute o comando a seguir para listar os contêineres.

  ```
  swift list
  ```
  {: pre}

4. Para evitar a destruição de dados por sobrescrições não intencionais, [configure o controle de versão do objeto](/docs/services/ObjectStorage/os_versioning.html). Se você não desejar o controle de versão de objetos, liste seus arquivos existentes no armazenamento e, se necessário, renomeie o diretório ou os arquivos antes de fazer o upload.

5. Faça upload de um arquivo para seu contêiner executando o comando a seguir.

  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

  **Nota**: para fazer upload de arquivos maiores do que 5 GB, [etapas extras são necessárias](/docs/services/ObjectStorage/os_large_files.html).

6. Opcional: para verificar se o upload foi bem-sucedido, visualize o conteúdo do seu contêiner executando o comando a seguir.

  ```
  swift list <container_name>
  ```
  {: pre}
