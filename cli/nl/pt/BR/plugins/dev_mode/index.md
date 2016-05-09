---

 

copyright:

  years: 2015，2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CLI do modo de desenvolvimento
{: #devmodecli}

*Última atualização: 11 de abril de 2016*

Com a interface da linha de comandos do modo de desenvolvimento do Bluemix (CLI dev_mode), é possível atualizar seus apps enquanto eles estão sendo executados na nuvem. A CLI dev_mode é construída como um plug-in de CLI cf
e suporta ambos os apps Liberty e IBM Node.js.
{: shortdesc}
 

É possível executar as tarefas a seguir com a CLI dev_mode:
- Alternação entre modo dev e modo normal de seu app.
- Atualização de arquivos do aplicativo incrementalmente sem um novo push.
- Inicialização, interrompimento ou reinicialização de seu app no contêiner existente.

## Instalando o plug-in dev_mode
**Pré-requisito:** Antes de iniciar, instale a CLI do Cloud Foundry. Consulte
[Começar a codificar com a interface de linha de comandos do Cloud Foundry](https://github.com/cloudfoundry/cli) para obter
detalhes. 


Use um dos métodos a seguir para instalar a ferramenta de linha de comandos dev_mode:
- Instalar localmente.
  1. Faça o download do plug-in dev_mode para sua plataforma a partir do [Repositório de
Plug-ins de CLI do IBM Bluemix](http://plugins.{DomainName}).
  2. Instale o plug-in dev_mode usando o comando cf install-plugin:
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Instale a partir do repositório da CLI do Bluemix.
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

## Visualizando comandos do dev_mode
**Pra exibir todos os comandos da CLI dev_mode, use o comando a seguir:**

```
cf plugins
```

## Índice de comandos da CLI dev_mode
{: #dev_mode_cmds_index}

Use o índice na tabela a seguir para referir-se aos comandos da CLI dev_mode usados frequentemente:

<table summary="índice de comandos do dev_mode">
 <thead>
 <th colspan="4">Comandos do dev_mode</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[help](#help)</td> 
 <td>[mode](#mode)</td> 
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr> 
 <tr> 
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody> 
 </table> 
*Tabela 1. Comandos do dev_mode*



## help
{: #help}

Exibe a ajuda sobre um comando.

```
cf help <commandName>
```


## mode
{: #mode}

Muda o modo do app.

```
cf mode <appName> <dev|normal>
```
<strong>Opções de comando</strong>:

   <dl>
   <dt>dev</dt>
   <dd>Modo de desenvolvimento.</dd>
   <dt>normal</dt>
   <dd>Modo de produção.</dd>
   </dl>


## status
{: #status}

Mostre o status do tempo de execução e do modo do app.
```
cf status <appName>
```



## update-file
{: #update_file}

Atualiza os arquivos de aplicativo na nuvem.

```
cf update-file <remotePath> <localPath> [command_options]
```


<strong>Opções de comando</strong>:

   <dl>
   <dt>expandir</dt>
   <dd>Indica se os arquivos transferidos por upload devem ou não ser extraídos do arquivo zip.</dd>
   <dt>reinício</dt>
   <dd>Reinicializa o tempo de execução do app depois que os arquivos são atualizados.</dd>
   </dl>


  
## delete-file
{: #delete_file}

Exclui os arquivos do aplicativo na nuvem.

```
cf delete-file <remotePath> [command_options]
```


<strong>Opções de comando</strong>:
 <dl>
   <dt>reinício</dt>
   <dd>Reinicializa o tempo de execução do app depois que os arquivos são atualizados.</dd>
  </dl>


## start-inplace
{: #start_inplace}
Inicializa o app no contêiner existente.

```
cf start-inplace <appName>
```



## stop-inplace
{: #stop_inplace}
Interrompe o app no contêiner existente.

```
cf stop-inplace <appName>
```



## restart-inplace
{: #restart_inplace}

Reinicializa o app no contêiner existente.

```
cf restart-inplace <appName>
```



# Links Relacionados
{: #rellinks}

## Links Relacionados
{: #general}

<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->


* [Ferramentas de CLI e de desenvolvimento](../../index.html#cli){:new_window}


