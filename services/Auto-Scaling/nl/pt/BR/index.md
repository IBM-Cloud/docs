---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao serviço {{site.data.keyword.autoscaling}}
{: #autoscaling}
Última atualização: 2 de novembro de 2016
{: .last-updated}

No {{site.data.keyword.Bluemix_notm}}, é possível gerenciar automaticamente a capacidade de seu aplicativo. Use o serviço {{site.data.keyword.autoscaling}} para aumentar ou diminuir automaticamente
a capacidade de cálculo de seu aplicativo. O número de instâncias do aplicativo é ajustado
dinamicamente com base na política do {{site.data.keyword.autoscaling}} que você define.
{:shortdesc} 

## Conteúdos
  * [Usando o serviço {{site.data.keyword.autoscaling}} no {{site.data.keyword.Bluemix_notm}}](#as-service)
  * [Configurando aplicativos Node.js com o serviço {{site.data.keyword.autoscaling}}](#node-asagent)
  * [Gerenciar o serviço {{site.data.keyword.autoscaling}} por meio da API RESTful](#RESTAPI)
  * [Gerenciar o serviço {{site.data.keyword.autoscaling}} por meio da CLI do {{site.data.keyword.autoscaling}}](#CLI)
  * [Campos de política para o serviço {{site.data.keyword.autoscaling}}](#policy_fields)
  * [Mensagens de erro](#err_msg)

## Usando o serviço {{site.data.keyword.autoscaling}} no {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Para usar o serviço
{{site.data.keyword.autoscaling}},
conclua as etapas a seguir:

1. No Painel do {{site.data.keyword.Bluemix_notm}}, clique em *Incluir um serviço ou API* e, em seguida, selecione o serviço {{site.data.keyword.autoscaling}} a partir da seção DevOps no catálogo de serviços. Uma nova janela é exibida para apresentar uma visão geral do serviço {{site.data.keyword.autoscaling}}.
2. Selecione o aplicativo ao qual deseja ligar o serviço {{site.data.keyword.autoscaling}} e clique em *Criar*. <br/>
*Lembre-se:* é possível ligar somente UM serviço {{site.data.keyword.autoscaling}} a um aplicativo. Se o aplicativo já está vinculado a outro serviço {{site.data.keyword.autoscaling}}, não selecione o aplicativo nesta etapa. Caso contrário, você obterá o erro CWSCV2004E.<br/>A janela Remontar aplicativo é exibida.
3. Na janela Remontar aplicativo, clique em *Remontar* para remontar seu aplicativo antes de usar o novo serviço {{site.data.keyword.autoscaling}} recém-incluído. <br/><ul><li>Para o aplicativo Liberty, o {{site.data.keyword.autoscaling}} está configurado automaticamente
e pronto para uso após a remontagem do aplicativo.</li> <li>Para aplicativos Node.js, deve-se atualizar
o código do aplicativo para ativar o serviço {{site.data.keyword.autoscaling}} antes de enviar o aplicativo por push para o {{site.data.keyword.Bluemix_notm}}. Veja [Configurando aplicativos Node.js com o serviço {{site.data.keyword.autoscaling}}](index.html#node_asagent) para obter mais detalhes.</ul><br/>
Após a nova preparação do aplicativo ser concluída, será possível iniciar a configuração
do serviço {{site.data.keyword.autoscaling}} para o aplicativo.
4. Para configurar o {{site.data.keyword.autoscaling}} para um aplicativo, na interface com o usuário do
{{site.data.keyword.Bluemix_notm}}, clique em seu aplicativo ao qual o serviço do {{site.data.keyword.autoscaling}} está ligado.
5. Na seção de serviços no Painel, clique no
						ícone *Auto-Scaling*.
6. Caso ainda não tenha feito isso, defina a política de {{site.data.keyword.autoscaling}} para o aplicativo clicando em *Criar política de {{site.data.keyword.autoscaling}}*.

Agora, é possível configurar a política de {{site.data.keyword.autoscaling}},
ver as estatísticas de métrica ou visualizar o histórico de ajuste de escala para o aplicativo.
<dl>
<dt>Configuração de política</dt>
<dd>Use essa seção para criar ou editar as regras de ajuste de escala para especificar as condições nas quais determinadas atividades de ajuste de escala devem ser acionadas.<ul>
<li> Para aplicativos Liberty for Java™, é possível definir regras de ajuste de escala para Heap, Memória, Tempo de resposta e Rendimento.  
<li> Para aplicativos Node.js, é possível definir regras de ajuste de escala para Heap, Memória e Rendimento.
<li> Para
aplicativos Ruby, é possível definir regras de ajuste de escala para Memória.</ul>
*Nota:* É possível definir várias regras de ajuste de escala para mais de um tipo de métrica. No entanto, o serviço {{site.data.keyword.autoscaling}} não detecta conflitos entre as políticas de ajuste de escala. Ao definir a política de ajuste de escala, devem-se assegurar que
							as múltiplas regras de ajuste de escala não entrem em conflito umas com as outras. Caso contrário, você pode ver o número total de instâncias flutuar porque o aplicativo diminui a escala em um minuto e aumenta a escala no minuto seguinte.<br/><br/>
Se a carga de trabalho de seu aplicativo muda dramaticamente durante o horário de pico e o horário sobressalente, é possível criar um planejamento de ajuste de escala para manipular os	diferentes requisitos de ajuste de escala para os diferentes períodos de tempo. Use o parâmetro Minimum Instance Count especificado em um planejamento para definir a linha de base do número de instâncias do aplicativo, embora as regras de ajuste dinâmico de escala ainda se apliquem ao planejamento para acionar as ações para diminuir a escala e aumentar a escala.</dd>
<dt>Estatísticas de métrica</dt>
<dd>Exibe as estatísticas de métrica para as instâncias de seu aplicativo. É possível ver a média de estatísticas e selecionar uma instância específica para
ver sua estatística.</dd>
<dt>Histórico de ajuste de escala</dt>
<dd>Exibe o histórico de ajuste de escala de seus aplicativos.<ul>
<li> Semana passada:
Exibe o histórico de ajuste de escala para a semana passada.
<li> Mês passado:
Exibe o histórico de ajuste de escala para o mês passado.
<li> Intervalo
customizado: é possível configurar o período.</ul>
*Nota:* É possível filtrar o registro de histórico selecionando Status de ajuste de escala ou Aumento/diminuição de ajuste de escala.</dd>
</dl>


## Configurando aplicativos Node.js com o serviço {{site.data.keyword.autoscaling}}
{: #node-asagent}

Para ativar o serviço {{site.data.keyword.autoscaling}} com seus apps Node.js, além das etapas de provisão e ligação do serviço, é necessário concluir as etapas a seguir também antes de enviar o app por push para {{site.data.keyword.Bluemix_notm}}.

1. Atualize o arquivo package.json com as etapas a seguir: <ol><li>Crie uma entrada de dependência para o `blumix-autoscaling-agent`, por exemplo `"bluemix-autoscaling-agent": "*"`.<br/><li>(Opcional) Configure o limite de heap na seção `scripts` com base na memória alocada para o aplicativo, por exemplo `"start": "node --max-old-space-size=600 app.js"`. .<br/>*Nota:* configure um valor para `max-old-space-size` se desejar acionar o ajuste de escala com base no uso do heap. Se o valor não for configurado ao iniciar seu aplicativo, o limite de heap padrão do Node.js de 1.4 GB será usado, independentemente de quanta memória está alocada para o aplicativo, que pode levar a decisões de ajuste automático de escala inadequadas.<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. Atualize seu arquivo principal para incluir a declaração do agente `var as_agent = require('bluemix-autoscaling-agent');`. O fragmento de código a seguir mostra um
arquivo js de entrada completo com a declaração do agente de ajuste automático de escala.<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## Gerencie o serviço {{site.data.keyword.autoscaling}} por meio da API RESTful 
{: #RESTAPI}

{{site.data.keyword.autoscaling}} A API RESTful fornece uma maneira alternativa de gerenciar o serviço {{site.data.keyword.autoscaling}}
além da UI do Bluemix e ela também suporta a recuperação e análise
de dados de ajuste de
escala. Ela fornece funcionalidades semelhantes, tais como a Criação de uma Política e a Obtenção
do Histórico de Ajuste de Escala, como na UI do {{site.data.keyword.Bluemix_notm}} com
API.

Para usar a API RESTful do {{site.data.keyword.autoscaling}} para gerenciar o serviço {{site.data.keyword.autoscaling}}, conclua os pré-requisitos a seguir: ligue o serviço {{site.data.keyword.autoscaling}} ao seu aplicativo, conforme especificado na seção anterior, adquira o `AccessToken`, a URL do servidor de API {{site.data.keyword.autoscaling}}
e o `app_id` do aplicativo que você deseja efetuar aumento ou diminuição de escala:

1. Para propósitos de segurança, em cada cabeçalho da solicitação da API RESTful do {{site.data.keyword.autoscaling}}, um `AccessToken`
apropriado, obtido por meio do procedimento CloudFoundry UAA, deve ser fornecido no cabeçalho `Authorization` para indicar a validação necessária da solicitação. A falha
em cumprir com este `AccessToken` resulta em uma resposta 401 Não autorizado. Há
duas maneiras de obter este `AccessToken` após instalar a ferramenta de linha
de comandos do Cloud Foundry e ter efetuado login no {{site.data.keyword.Bluemix_notm}}:<ul><li>é possível obter este token por meio do comando `cf oauth-token`:
   ```
   > cf oauth-token
   Obtendo token de OAuth...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
 A sequência longa retornada que inicia com “bearer” é o AccessToken que pode ser usado na
solicitação da API RESTful do {{site.data.keyword.autoscaling}}. Se você encontrar erros,
tais como “Comando não localizado”, poderá atualizar sua ferramenta de linha de comandos do
Cloud Foundry para uma versão mais recente.</li><li>Também é possível localizar este AccessToken
no diretório inicial. Após ter efetuado login no {{site.data.keyword.Bluemix_notm}} a
partir da interface da linha de comandos, uma pasta `.cf` é criada em sua pasta
inicial, na qual é possível localizar um nome de arquivo JSON `config.json` que
contém uma lista das informações do ambiente de criação de log atual,
tais como organização, espaço,
terminal de autenticação e versão. É possível localizar uma entrada `AccessToken`
no arquivo conforme a seguir: 
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
O `AccessToken` no `config.json` é válido apenas por um período de tempo. Se
você obtiver uma resposta 401 Não autorizado para
solicitação de API REST, poderá precisar efetuar
login novamente a partir da interface da linha de comandos para atualizar o arquivo e obter o novo
`AcessToken`. </li></ul>
 
2.  É possível obter a URL do servidor de API {{site.data.keyword.autoscaling}}
ao verificar a variável de ambiente `VCAP_SERVICE` após ligar seu aplicativo
com o serviço {{site.data.keyword.autoscaling}}. No `VCAP_SERVICE`, é possível localizar a seção do serviço {{site.data.keyword.autoscaling}} e a `api_url`
é a URL do servidor de API com a qual seu aplicativo esta ligado. Você precisa desta URL do servidor
de API para conectar-se ao serviço da API RESTful do {{site.data.keyword.autoscaling}}:
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
  Observe que esta url também pode ser localizada por meio do comando `cf env APPNAME`:
   ```
   > cf env Hello
   Obtendo variáveis env para app Hello em org OE_Runtimes_SVT / space RT_SVT como Alice...
   OK

   System-Provided:
   {
     "VCAP_SERVICES": {
     "Auto-Scaling": [
      {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  É possível obter o `app_id` a partir da variável de ambiente `VCAP_SERVICES` ou apenas execute o comando `cf app APPNAME --guid`:

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

Com todos os pré-requisitos acima, agora é possível fazer a solicitação da API REST usando
o complemento RestClient no navegador ou apenas por meio de alguma ferramenta, como `curl`. 

Com o Complemento do Cliente REST, como aqueles para Firefox ou Chrome, é possível acionar a solicitação REST para o servidor de API {{site.data.keyword.autoscaling}} para executar seu
comando. Você fornece apenas estes complementos com a URL da API REST, o método e cabeçalhos que são necessários por esta API REST e os parâmetros na parte do corpo. Para obter mais detalhes sobre cada
API, veja [API Rest
do IBM {{site.data.keyword.autoscaling}} para {{site.data.keyword.Bluemix_notm}}](https://new-console.ng.bluemix.net/apidocs/48){:new_window}.

Com ferramentas como o `curl`, é possível gerenciar o serviço {{site.data.keyword.autoscaling}} dentro de um script, conforme a seguir:    
```
    cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)

    echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## Gerencie o serviço
{{site.data.keyword.autoscaling}} por meio da CLI do {{site.data.keyword.autoscaling}} 
{: #CLI}

A CLI do {{site.data.keyword.autoscaling}} fornece funcionalidades semelhantes às
da API RESTful do {{site.data.keyword.autoscaling}} de uma maneira mais amigável de
configurar o serviço {{site.data.keyword.autoscaling}}. Com a CLI do {{site.data.keyword.autoscaling}}, você não precisa se preocupar com os detalhes na API RESTful do {{site.data.keyword.autoscaling}}, tais como `AccessToken`
e a URL do servidor de API. Tudo o que você é apenas seguir as orientações passo a passo que
a CLI fornece. Para obter mais detalhes sobre como instalar e usar a CLI do {{site.data.keyword.autoscaling}},
veja [CLI do {{site.data.keyword.autoscaling}}](../../cli/plugins/auto-scaling/index.html){:new_window}



## Campos de política para o serviço {{site.data.keyword.autoscaling}}
{: #policy_fields}

| Nome do campo  | Descrição |
|-------------|----------------------|
|*Contagem máxima permitida de
instâncias* |	O número máximo das instâncias do aplicativo que podem ser
iniciadas. Se o número atual das instâncias do aplicativo for igual a esse valor, o serviço {{site.data.keyword.autoscaling}} não aumentará mais a escala do aplicativo. Contagem mínima de instâncias padrão. O número mínimo de instâncias do aplicativo que podem ser iniciadas. Se o número das instâncias for igual a esse valor, o serviço
{{site.data.keyword.autoscaling}} não diminuirá mais a escala do aplicativo. |
| *Tipo de métrica*	| 	Os tipos de métrica suportados que podem ser
monitorados. Para obter informações adicionais, veja a Tabela 2. |
| *Ampliar escala* | 	Especifica o limite que aciona uma ação de aumento de escala e quantas instâncias são aumentadas quando a ação de aumento de escala é acionada. |
| *Reduzir escala* |	Especifica um limite que aciona uma ação de diminuição de escala e quantas instâncias são
diminuídas quando a ação de diminuição de escala é acionada. |
| *Janela de estatística* |	A duração do período passado quando os valores da métrica recebidos são reconhecidos como válidos. Os valores da métrica
são válidos somente se os registros de data e hora estiverem dentro desse período. A unidade do parâmetro Statistic Window é segundo. |
| *Duração da violação*	| A duração do período passado quando uma ação de ajuste de escala pode ser acionada. Uma ação de ajuste de escala é acionada quando os valores da métrica coletados estão acima do
limite superior ou abaixo do limite inferior maior que o tempo especificado. A unidade do parâmetro Breach Duration é segundo. |
| *Período de espera para diminuir o ajuste de escala* | Depois que uma ação de diminuição de ajuste de escala ocorre, outras solicitações de ajuste de escala são ignoradas durante o período especificado pelo parâmetro Cooldown period for scaling in. A unidade desse parâmetro é segundo. |
| *Período de espera para aumentar o ajuste de escala*	| Depois que uma ação de aumento de ajuste de escala ocorre, outras solicitações de ajuste de escala são ignoradas durante o período especificado pelo parâmetro Cooldown period for scaling. A unidade desse parâmetro é segundo. |
| *Fuso horário*	| O fuso horário em que o planejamento se aplica. |
| *Horário de início*  |	O horário de início de um planejamento recorrente. |
| *Horário de encerramento*    |	O horário de encerramento de um planejamento recorrente.	|
| *Repetir em*	|	O dia da semana em que se aplica um planejamento recorrente. |
| *Contagem mínima de instâncias* |	O número mínimo de instâncias que podem ser iniciadas para o aplicativo
durante o período de tempo especificado no planejamento. |
| *Data e hora de início* |	A data e hora de início do planejamento configurado em uma data
específica. |
| *Data e hora de encerramento* |	A data e hora de encerramento do planejamento configurado em uma data específica.	|

Tabela 1. Campos de política na política de ajuste de escala

| Nome da métrica | Descrição | Tipo de aplicativo
suportado |
|-------------|----------------------| ------------------- |
| *Heap* |	A porcentagem de uso da memória heap.	| Liberty for Java, SDK do Node.js |
| *Memória*   |	A porcentagem de uso da memória.	|  All |
| *Rendimento* | O número das solicitações processadas por
segundo.| Liberty for Java, SDK do Node.js |
| *Tempo de resposta* |	O tempo de resposta das
solicitações processadas.	| Liberty for Java |

Tabela 2. Nomes de métricas suportados

*Nota:* para coletar dados de métrica de Auto-scaling, seu aplicativo deve ser implementado como aplicativo da web do Liberty para que a medição de solicitações HTTP/HTTPS seja processada pelo contêiner da web do Liberty.
Por exemplo, se executar um aplicativo Spring Boot como um app de "Classe principal", o buildpack do Liberty só fornecerá ambiente Java para você e o app realmente será executado no contêiner Tomcat integrado, portanto, nenhum dado de métrica será coletado pelo serviço de ajuste automático de escala. Deve-se executar o app como um archive web do Liberty para que funcione com o serviço de ajuste automático de escala.

## Mensagens de erro
{: #err_msg}
Esta seção lista as mensagens de aviso e erro que são produzidas pelo serviço {{site.data.keyword.autoscaling}}.
 
### CWSCV2004E Outro serviço {{site.data.keyword.autoscaling}} já está vinculado
ao aplicativo.
**É possível ligar somente um serviço {{site.data.keyword.autoscaling}} a um aplicativo. Esse erro ocorre quando você deseja ligar o serviço {{site.data.keyword.autoscaling}} a um aplicativo que já está ligado a outro serviço {{site.data.keyword.autoscaling}}.**

Selecione outro aplicativo sem qualquer outro serviço {{site.data.keyword.autoscaling}} vinculado e vincule o serviço {{site.data.keyword.autoscaling}} de destino a esse aplicativo.
Se você encontrar esse erro em todos os outros casos, entre em contato com o suporte IBM.

### CWSCV6001E O servidor de API não pode analisar as sequências JSON de entrada para API: {0}.
**O problema ocorre ao analisar sequências JSON de entrada.**

Verifique o documento JSON de entrada com API e corrija o erro contido nele.

### CWSCV6002E O servidor API não pode analisar as sequências JSON de saída para API: {0}.
**O problema ocorre ao analisar sequências JSON de entrada.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6003E Erro do formato de sequências JSON de entrada: {0} no JSON de entrada para API: {1}.
**Erro de formatação localizado ao analisar as sequências JSON de entrada.**

Verifique o documento JSON de entrada com API e corrija o erro contido nele.

### CWSCV6004E Erro do formato de sequências JSON de saída: {0} no JSON de saída para API: {1}.
**Erro de formatação localizado ao analisar as sequências JSON de saída.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6005E Ocorreu um erro interno do servidor durante {0}.
**Ocorre o erro interno de servidor ao processar a solicitação.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6006E Falha ao chamar APIs CloudFoundry: {0}
**Ocorreu um erro ao chamar as APIs CloudFoundry.**

Entre em contato com o Administrador em nuvem para obter mais informações.

### CWSCV6007E O aplicativo não foi localizado: {0}
**O aplicativo não foi localizado.**

Verifique as informações do aplicativo para obter mais informações.

### CWSCV6008E Ocorreu o erro a seguir ao recuperar as informações para o aplicativo {0}: {1}
**A recuperação de informações do aplicativo falhou com certos erros.**

Verifique as informações do aplicativo para obter mais informações.

### CWSCV6009E Serviço: {0} para App {1} não foi localizado.
**O serviço para esse aplicativo não pode ser localizado.**

Verifique a ligação de serviços para este aplicativo para obter mais informações.

### CWSCV6010E A política para App {0} não foi localizada
**A política para esse aplicativo não pode ser localizada.**

Verifique a configuração de aplicativo para obter mais informações.

### CWSCV6011E A Autenticação Interna falhou durante {0}
**Falha na autenticação interna.**

Entre em contato com o Administrador em nuvem para obter mais informações.


# rellinks
{: #rellinks}

## SAMPLEs
{: #samples}

* [Tutorial: Torne seu aplicativo elástico no {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Laboratórios da Arquitetura Cloud Foundry](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [API REST do IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://new-console.{DomainName}/apidocs/48){:new_window}

## gerais
{: #general}

* [Ajuste de escala de contêineres](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [Ajuste de escala de servidores virtuais](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}}CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [Agente do {{site.data.keyword.autoscaling}} para o Node.js](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

