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

# Trabalhando com diretórios

O Swift não tem uma estrutura de diretório verdadeira, mas usa nomenclatura para
representar um layout de diretório. Se você especificar um nome de diretório, ele será anexado a todos os nomes de arquivo como parte do caminho relativo.
{: shortdesc}

## Incluindo um diretório em um contêiner com a CLI Swift

Para incluir um diretório em um contêiner, deve-se ter a estrutura de diretório no local em seu dispositivo local.

1. Localmente, crie um diretório e salve o seu arquivo.
2. Execute o comando a seguir para fazer upload de um diretório para seu contêiner.

    ```
    swift upload <container_name> <directory_name>
    ```
    {: pre}

## Fazendo download de um diretório com a CLI
Para fazer download de uma estrutura de diretório, use o parâmetro `-prefix` para indicar o diretório ou a estrutura de diretório da qual você deseja fazer download.

1. Execute o comando a seguir para fazer download de um diretório.

    ```
    swift download <container_name> --prefix <directory>
    ```
    {: pre}
