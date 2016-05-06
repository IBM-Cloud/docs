---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# CLI do modo de desenvolvimento
{: #devmodecli}

*Última atualização: 25 de fevereiro de 2016*

O modo de desenvolvimento (dev_mode) é um recurso do Bluemix que é possível usar para trabalhar com seus apps enquanto são executados na nuvem. O modo de desenvolvimento inclui a interface de linha de comandos dev_mode. A CLI dev_mode é construída como um plug-in de CLI cf
e suporta ambos os apps Liberty e IBM Node.js.

A CLI dev_mode fornece os recursos a seguir:
- Alternação entre modo dev e modo normal de seu app.
- Atualização de arquivos do aplicativo incrementalmente sem um novo push.
- Inicialização, interrompimento ou reinicialização de seu app no contêiner existente.

## Introdução
**Pré-requisito:** Antes de iniciar, instale a CLI do Cloud Foundry. Consulte
[Começar a codificar com a interface de linha de comandos do Cloud Foundry](https://github.com/cloudfoundry/cli) para obter
detalhes. 


Use um dos métodos a seguir para instalar a ferramenta de linha de comandos dev_mode:
- Instalar localmente.
  1. Faça o download do plug-in dev_mode para sua plataforma a partir do [Repositório de
Plug-ins de CLI do IBM Bluemix](http://plugins.ng.bluemix.net).
  2. Instale o plug-in dev_mode usando o comando cf install-plugin:
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Instalar a partir do repositório de CLI do Bluemix.
  1. Inclua o repositório bluemix-repo nos repositórios de CLI do Cloud Foundry usando o comando a seguir:
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Digite cf repo-plugins. O plug-in dev_mode aparecerá no repositório bluemix-repo.
		
		```
        cf repo-plugins
        ```
  
  3. Instale o plug-in dev_mode nos plug-ins de CLI do Cloud Foundry usando o comando a seguir:
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Uso
**Para exibir todos os comandos de CLI do dev_mode, use o comando a seguir:**

```
cf plugins
```

### Comandos do dev_mode

### mode

```
cf mode <appName> <dev|normal>
```

Muda o modo do app.

### status

```
cf status <appName>
```

Mostre o status do tempo de execução e do modo do app.

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

Atualiza os arquivos de aplicativo na nuvem.

Opções de comando:

**expand**

Indica se os arquivos transferidos por upload devem ou não ser extraídos do arquivo zip.

**restart**

Reinicializa o tempo de execução do app depois que os arquivos são atualizados.
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

Exclui os arquivos do aplicativo na nuvem.

Opções de comando:

**restart**

Reinicializa o tempo de execução do app depois que os arquivos são excluídos.

### start-inplace

```
cf start-inplace <appName>
```

Inicializa o app no contêiner existente.

### stop-inplace

```
cf stop-inplace <appName>
```

Interrompe o app no contêiner existente.

### restart-inplace

```
cf restart-inplace <appName>
```

Reinicializa o app no contêiner existente.



### help

```
cf help <commandName>
```
Exibe a ajuda sobre um comando.
