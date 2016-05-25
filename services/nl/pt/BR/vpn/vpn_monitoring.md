---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitorando o status e o fluxo de tráfego
{: #monitor}  
*Última atualização: 17 de março de 2016*  

Use o recurso de monitoramento para visualizar o status da conexão e a taxa de fluxo de tráfego entre o gateway VPN no local ou do servidor SoftLayer e o gateway {{site.data.keyword.vpn_short}}. 
{:shortdesc}  
##Monitoramento no painel de serviço
{: #dashboard}

Selecione a guia **Monitoramento** para visualizar as estatísticas de conexão a seguir.

* **Status da conexão:** Status da conexão VPN entre o gateway VPN no local ou do servidor SoftLayer e o gateway IBM VPN. Valores: 1=UP, -1=DOWN 
* **Taxa de tráfego de saída em bytes/segundo e pacotes/segundo:** Taxa de tráfego do gateway IBM VPN para o gateway VPN no local ou do servidor SoftLayer.  
* **Taxa de tráfego de entrada em bytes/segundo e pacotes/segundo:** Taxa de tráfego do gateway VPN no local ou do servidor SoftLayer para o gateway IBM VPN.  

As estatísticas de monitoramento são exibidas como gráficos com dados das últimas 48 horas. Os gráficos são atualizados automaticamente a cada 20 minutos. No entanto, é possível buscar os dados mais recentes a qualquer momento alternando da guia de monitoramento e retornando a ela.

**Nota:** os gráficos usam o horário da Hora Universal Coordenada (UTC) e não o horário local.  
##Monitoramento no Logmet
{: #logmet}

Use o [Logmet](https://logmet.{DomainName}) para visualizar estatísticas detalhadas de conexão. 

1. Efetue login com suas credenciais do Bluemix e o nome do espaço e da organização em que você criou a instância de serviço IBM VPN.  
2. Selecione o ícone de pasta (![](images/folder.png)) na parte superior direita.
3. Selecione **Monitoramento do serviço VPN** na lista de painéis para visualizar os gráficos. Os gráficos usam o horário local.  

**Nota:** deve-se selecionar a guia **Monitoramento** no painel de serviço IBM VPN pelo menos uma vez para enviar uma consulta ao Logmet para criar o painel de serviço VPN no Logmet. O Logmet demora até 10 minutos depois que você estabelecer a conexão VPN para mostrar as estatísticas de conexão.


