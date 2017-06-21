---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Resolução de problemas para tempos de execução
{: #runtimes}

Você pode ter problemas ao usar tempos de execução do {{site.data.keyword.Bluemix}}. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{:shortdesc}


## Buildpack obsoleto usado quando um aplicativo é enviado por push
{: #ts_loading_bp}

É possível que você não consiga usar os componentes de buildpack mais recentes
ao enviar um app por push. É possível usar buildpacks que possuem mecanismos integrados
para evitar o carregamento de componentes obsoletos ou é possível excluir os conteúdos
no diretório de cache do app antes de enviar por push ou remontar o app. 

Ao enviar por push ou remontar um app após a atualização do buildpack, os componentes de buildpack mais recentes não são carregados automaticamente. Como resultado, o seu aplicativo usa os componentes de buildpack obsoletos a partir do cache. As atualizações que foram aplicadas ao buildpack desde a última vez que o app foi enviado por push não são implementadas. 
{: tsSymptoms}

Alguns buildpacks não são configurados para fazer download automaticamente de todos os componentes atualizados da Internet para assegurar que você sempre use a versão mais recente.
{: tsCauses} 

É possível usar buildpacks que tenham mecanismos integrados para evitar o carregamento de componentes obsoletos, por exemplo, os buildpacks a seguir: 
{: tsResolve}

  * [Buildpack Java do Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/java-buildpack){: new_window}. Esse buildpack tem um mecanismo integrado para assegurar que a versão mais recente do buildpack seja usada. Para obter mais informações sobre como esse mecanismo funciona, veja [extending-caches.md ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Buildpack Node.js do Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Esse buildpack fornece funcionalidade semelhante ao usar variáveis de ambiente. Para que o buildpack Node.js sempre possa fazer download de módulos do nó a partir da Internet, digite o comando a seguir na interface de linha de comandos cf: 	
  ```
  set NODE_MODULES_CACHE=false
  ```

Se o buildpack que você estiver usando não fornecer um mecanismo para carregar os componentes mais recentes automaticamente, será possível excluir manualmente o conteúdo no diretório de cache e enviar por push seu app novamente. Use as seguintes etapas:

 1. Efetue o check-out de uma ramificação de um buildpack nulo, por exemplo, https://github.com/ryandotsmith/null-buildpack. Para obter informações sobre como verificar uma ramificação, veja [Conceitos básicos do Git - Obtendo um repositório Git ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
 2. Inclua a linha a seguir no arquivo `null-buildpack/bin/compile`
e confirme as mudanças. Para obter informações sobre como confirmar mudanças, veja [Conceitos básicos do Git - Registrando mudanças no repositório ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
 3. Envie seu app por push com o buildpack nulo que foi modificado para excluir
o cache usando o comando a seguir. Depois de concluir essa
etapa, todos os conteúdos no diretório de cache de seu app serão excluídos.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. Envie seu app por push com o buildpack mais recente que você deseja usar
usando o comando a seguir: 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
 
## Mensagens de AVISO do buildpack PHP
{: #ts_phplog}

Talvez você veja mensagens que contenham AVISO nos logs. É possível parar a criação de log dessas mensagens alterando o
nível de criação de log.	

Ao enviar um app por push para o {{site.data.keyword.Bluemix_notm}} usando um buildpack PHP, será possível ver mensagens contendo `NOTICE`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
No buildpack PHP, o parâmetro error_log define o nível de criação de log. Por padrão, o valor do parâmetro `error_log`
é **stderr notice**. O exemplo a seguir mostra a configuração do nível de criação de log padrão no arquivo `nginx-defaults.conf` do buildpack PHP que é fornecido pelo Cloud Foundry. Para obter mais informações, veja [cloudfoundry/php-buildpack ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
As mensagens `NOTICE` são para informações e podem não indicar um problema. É possível parar a criação de log dessas mensagens mudando o nível de criação de log de `stderr notice` para `stderr error` no arquivo nginx-defaults.conf de seu buildpack. Por
exemplo: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Para obter mais informações sobre como mudar a configuração de criação de log padrão, veja [error_log ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Não é possível importar uma biblioteca Python de terceiros para o {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Pode ser que você não consiga importar uma biblioteca Python de terceiros
para o {{site.data.keyword.Bluemix_notm}}. Para resolver o problema, inclua arquivos de configuração no diretório-raiz de seu app python.

Ao tentar importar uma biblioteca Python de terceiros, como
a biblioteca `web.py`, o comando `cf push`
falha.
{: tsSymptoms}

As informações de configuração para o app Python estão ausentes.
{: tsCauses}

Inclua um arquivo `requirements.txt` e um arquivo `Procfile` no diretório-raiz de seu app Python. As informações a seguir presumem que você
esteja importando a biblioteca `web.py`:
{: tsResolve}

 1. Inclua um arquivo `requirements.txt` no diretório-raiz de seu app Python.
 
 O arquivo `requirements.txt` especifica os pacotes de biblioteca necessários para o app Python e a versão dos pacotes. O exemplo a seguir mostra o conteúdo do arquivo `requirements.txt`, em que `web.py==0.37` indica que a versão da biblioteca `web.py` que será transferida por download é 0,37 e `wsgiref==0.1.2` indica que a versão da interface do gateway do servidor da web que é requerida pela biblioteca web.py é 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 Para obter mais informações sobre como configurar
o arquivo `requirements.txt`, consulte [Arquivos de requisitos](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
 2. Inclua um arquivo `Procfile` no diretório-raiz de seu app Python.
 O arquivo `Procfile` deve conter o comando inicial para seu app Python. No comando a seguir, *yourappname* é o nome de seu app Python e *PORT* é o número da porta que seu app Python deve usar para receber solicitações de usuários do app. *$PORT* é opcional. Se você não especificar PORT no comando inicial, o número da porta sob a variável de ambiente `VCAP_APP_PORT` que está dentro do app será usado. 
	```
	web: python <yourappname>.py $PORT
	```

Agora é possível importar a biblioteca Python de terceiros para o {{site.data.keyword.Bluemix_notm}}.	


## O botão Ações na página Detalhes da instância está desativado
{: #ts_actionsbutton}

O botão Ações na página Detalhes da instância está desativado.
{: tsSymptoms} 

Esse problema ocorre por causa dos motivos a seguir:
{: tsCauses}

 * O app não é um app da web Java&trade;. O Runtime Management Utilities (RMU) suporta apenas apps da web implementados com buildpacks Liberty.
 * O app não é implementado com o buildpack Liberty integrado.
 * O app foi implementado com uma versão anterior do buildpack Liberty.

Se o problema for causado por uma versão anterior do buildpack Liberty, reimplemente o app no {{site.data.keyword.Bluemix_notm}}. Caso contrário, é possível fornecer os
arquivos de log do aplicativo do cliente para a equipe de suporte:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## São necessárias credenciais para abrir uma janela de rastreio ou de dump
{: #ts_username}

Um nome de usuário e uma senha são necessários para abrir a janela de rastreio ou de dump.
{: tsSymptoms}

Esse problema ocorre por causa do tempo limite da sessão de login.
{: tsCauses}

Insira o nome do usuário e a senha novamente.
{: tsResolve}


## Ocorre um erro quando operações de rastreio ou de dump estão em execução
{: #ts_target}

Uma mensagem de erro é exibida quando as operações de rastreio ou dump
estão em execução. A mensagem indica que uma instância de destino para um app não está no estado em execução:	
{: tsSymptoms}

```
Instância 0: A especificação de rastreio foi configurada com êxito
Instância 2: A especificação de rastreio foi configurada com êxito.
Instância 1: A instância de destino 1 para o app abcd não está no estado de execução.
Instância 3: A especificação de rastreio foi configurada com êxito
Instância 4: A especificação de rastreio foi configurada com êxito
```

Esse problema ocorre por causa dos motivos a seguir:
{: tsCauses} 

  * Os recursos de gerenciamento de rastreio ou de dump são apenas para instâncias de app que estão em execução. As operações de rastreio ou de dump não podem ser usadas em instâncias do app que estejam paradas, sendo iniciadas ou que tenham sido interrompidas.
  * O status da instância do app está mudando quando o diálogo de rastreio ou de dump é aberto. 

Feche a janela e, em seguida, abra-a novamente.
{: tsResolve} 


## As instâncias possuem configurações traceSpecification diferentes
{: #ts_different_config}

Para instâncias diferentes de um app, é possível ver configurações traceSpecification diferentes.
{: tsSymptoms}

Esse comportamento ocorre por causa dos motivos a seguir:
{: tsCauses}

  * Você mudou a configuração de uma ou mais instâncias anteriormente. Se você mudar a configuração traceSpecification de uma instância, a mudança não se aplicará a outras instâncias do mesmo app. Por exemplo, seu app usa log4j e você tem 2 instâncias para esse app. É possível mudar o nível de log da instância 0 de informações para depuração, mas o nível de log da instância 1 permanecerá como informações.
  
  * O app é ampliado e possui novas instâncias. O RMU não se aplica à configuração traceSpecification da instância existente para a nova instância ampliada. A nova instância usa a configuração padrão. Por exemplo, seu app usa log4j e tem uma instância. É possível mudar o nível de log dessa instância de informações para depuração. Depois de fazer essa mudança, se você ampliar seu app para duas instâncias, o nível de log da nova instância será informações, em vez de depuração.

Nenhuma
ação foi necessária. Este comportamento é esperado.
{: tsResolve} 


## Cota do disco excedida
{: #ts_diskquota}

Você pode ver, em seu log de app, que sua cota do disco foi excedida.

Você vê a mensagem de erro `Cota do disco excedida` no log de seu app.
{: tsSymptoms}

Esse problema ocorre por causa de um dos motivos a seguir: 
{: tsCauses} 

  * Os arquivos de dump são gerados com as instâncias do app em execução e os arquivos usam até a cota de disco alocada. Por padrão, a cota de disco para uma instância de app é 1 GB. É possível verificar o uso de
seu disco clicando em **Painel>Aplicativo>Tempo de Execução do Aplicativo**. O exemplo a seguir mostra as informações de tempo de execução, incluindo uso do disco, de duas instâncias de um app:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Executando	1,0%	344,8 MB/512 MB	236,8 MB/1 GB
	2		Executando	2,3%	361,2 MB/512 MB	235,7 MB/1 GB
    ```
  * A cota do disco é limitada pela cota da organização atual.

Utilize um dos seguintes métodos:
{: tsResolve} 

  * Excluir arquivos de dump depois de eles serem transferidos por download.
  * Reimplementar o app com uma cota de disco maior, incluindo a entrada a seguir no manifest de implementação:
    ```
	disk_quota: 2048
	```
	
