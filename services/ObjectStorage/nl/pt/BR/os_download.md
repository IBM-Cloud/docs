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

# Fazendo download de objetos

É possível fazer download dos objetos armazenados para revisão ou edição por meio da UI ou da CLI.
{: shortdesc}


## Fazendo download de objetos da UI {: #downloading-ui}

1. Para evitar a destruição de dados por sobrescrições não intencionais, [configure o controle de versão do objeto](/docs/services/ObjectStorage/os_versioning.html). Se você não desejar a versão de objeto, renomeie o diretório ou os arquivos antes de fazer download, se necessário.
2. No painel da instância de serviço, selecione o contêiner com o arquivo do qual você deseja fazer download.
3. Selecione o arquivo.
4. No menu suspenso **Ações**, selecione **Fazer download de arquivo**.


## Fazendo download de objetos com a CLI Swift {: #downloading-cli}

1.  Se você não tiver efetuado login no {{site.data.keyword.Bluemix_notm}}, efetue login na organização e no espaço que contêm sua instância do {{site.data.keyword.objectstorageshort}}.

    ```
    cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
    ```
    {: pre}

2. Para evitar a destruição de dados por sobrescrições não intencionais, [configure o controle de versão do objeto](/docs/services/ObjectStorage/os_versioning.html). Se você não desejar o controle de versão de objetos, liste seus arquivos existentes no armazenamento e, se necessário, renomeie o diretório ou os arquivos antes de fazer o download.

3. Faça download de um arquivo executando o comando a seguir:

    ```
    swift download <container_name> <file_name>
    ```
    {: pre}
