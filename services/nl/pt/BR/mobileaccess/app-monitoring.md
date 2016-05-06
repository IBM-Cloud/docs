---

copyright:
  years: 2015, 2016
  
---

# Monitoramento de Aplicativo
{: #app-monitoring}

Além de recursos de segurança, o {{site.data.keyword.amafull}} também fornece monitoramento e análise para seus aplicativos móveis. É
possível registrar logs de clientes e monitorar dados com o {{site.data.keyword.amashort}} Client SDK. Os desenvolvedores podem controlar quando enviar esses dados para o serviço {{site.data.keyword.amashort}}. Todos os eventos de segurança, tais como sucesso ou falha de autenticação, que ocorrem no serviço {{site.data.keyword.amashort}} são registrados automaticamente.

Quando os dados são entregues para o {{site.data.keyword.amashort}}, é possível usar o Painel de monitoramento do {{site.data.keyword.amashort}} para obter insights da análise sobre seus aplicativos móveis, dispositivos e logs do cliente. As informações sobre solicitações que seu aplicativo faz aos recursos que são protegidos por {{site.data.keyword.amashort}} são registradas por padrão.

Os dados registrados automaticamente incluem informações como número de autenticações, novos dispositivos e novos usuários. Além disso, é
possível configurar o {{site.data.keyword.amashort}} Client SDK para relatar as informações a seguir:

### Estatísticas de uso de seus aplicativos móveis
{: #usage-stats}

É possível configurar seus aplicativos móveis para registrar eventos do ciclo de vida do aplicativo e enviar os dados registrados ao serviço {{site.data.keyword.amashort}} com algumas chamadas API simples. É possível registrar o número de
aberturas de apps, notificações push recebidas, etc.

### Captura de log do lado do cliente
{: #client-side-logcapture}

Aplicativos no campo ocasionalmente apresentam problemas que requerem atenção
do desenvolvedor para serem corrigidos. Muitas vezes é difícil reproduzir
esses problemas. <!--in R&D.--> Desenvolvedores que trabalharam no código podem não ter o
ambiente ou o dispositivo exato com o qual testar. Nessas situações,
é útil ter a capacidade de recuperar logs de depuração a partir de dispositivos
clientes conforme os problemas ocorrem no ambiente em que
acontecem.

## Preservando dados capturados
{: #preserve-captureddata}

Não há como garantir que todos os dados capturados sejam preservados no lado do cliente. Seus
usuários podem estar executando o aplicativo móvel offline e
acumulando simultaneamente dados analíticos e de log capturados. Como
o cliente está offline com espaço de sistema de arquivos limitado, eventos registrados
mais antigos devem ser limpos em favor da preservação de eventos registrados mais
recentemente. Cabe ao desenvolvedor decidir quando enviar dados capturados ao serviço {{site.data.keyword.amashort}} usando as APIs fornecidas.

## Usando o Painel de monitoramento do {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Abra o Painel do {{site.data.keyword.Bluemix}} e clique em seu aplicativo {{site.data.keyword.Bluemix_notm}}

2. Quando o painel do aplicativo {{site.data.keyword.Bluemix_notm}} for aberto, clique no ladrilho do {{site.data.keyword.amashort}}

3. No Painel do {{site.data.keyword.amashort}}, clique no link `Monitoramento` no menu à esquerda

## Próximas Etapas
{: #next-steps}
* [Ativando, configurando e usando o criador de logs](app-monitoring-logger.html)
* [Reunindo análise de uso](app-monitoring-gathering-analytics.html)
