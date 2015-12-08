
{:shortdesc: .shortdesc}

# Serviços VCAP

*Última atualização: 9 de novembro de 2015*


A variável de ambiente VCAP_SERVICES é um objeto JSON
que contém informações que podem ser usadas para interagir com uma instância de serviço
no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Recuperando o valor da variável de ambiente VCAP_SERVICES
{:retrieving}

A variável de ambiente VCAP_SERVICES é um objeto JSON
que contém informações que podem ser usadas para interagir com uma instância de serviço
no {{site.data.keyword.Bluemix_notm}}. As informações incluem o nome da instância de serviço, a credencial e a URL de conexão com a instância de serviço. Esses valores são preenchidos na variável de ambiente VCAP_SERVICES quando o seu aplicativo está ligado a uma instância de serviço no {{site.data.keyword.Bluemix_notm}}.

O valor da variável de ambiente VCAP_SERVICES está disponível somente ao ligar uma instância de serviço a seu aplicativo. É possível visualizar as variáveis de ambiente de aplicativo usando o driver do console WebSocket. O exemplo a seguir mostra como usar o driver do
console WebSocket para visualizar as variáveis de ambiente de um aplicativo Node.js.

Primeiro, execute o comando para enviar por push novamente o seu aplicativo Node.js.
```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp
```
Em seguida, insira a seguinte url:
```
https://yourapp.{APPDomain}/bash.sh
```
Na página que é exibida, clique na marca de seleção para conectar a ferramenta e, em seguida, emita o comando env para ver as variáveis de ambiente de seu aplicativo. Para obter informações adicionais sobre o cf-debug-tools,
consulte [Ferramentas de depuração para Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools).


## Visualizando camadas de infraestrutura do Bluemix
{:viewinfra}


O {{site.data.keyword.Bluemix_notm}} abstrai e oculta
camadas do sistema operacional e da infraestrutura, para que você não precise gerenciá-las. No entanto, às vezes
você pode desejar saber mais sobre o sistema operacional e o middleware para seu app.

É possível executar o comando cf stacks para mostrar as pilhas disponíveis, ou sistemas de arquivos raiz, em que seus apps devem ser implementados. É possível também especificar a pilha ao usar o comando cf push com a opção *-s* e o *stack_name*, em que stack_name é o sistema de arquivos raiz, como `lucid64` ou `cflinuxfs2`:
```
cf push appName -s stack_name
```
É possível usar o comando `cf buildpacks` para mostrar os componentes de middleware, como o perfil WebSphere Liberty e o SDK para Node.js, que estão disponíveis como tempos de execução para seu app ser executado. E você pode especificar o ambiente de tempo de execução para seu app usando o comando a seguir:
```
cf push appName -b buildpackname
```
