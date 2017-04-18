---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Introdução ao IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} é um serviço que facilita a rápida configuração em uma instância pré-configurada do WebSphere Application Server Liberty, do Traditional Network Deployment ou do Traditional WebSphere Java EE em um ambiente de nuvem hospedado no {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Visão geral do WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #overview}

O WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} fornece aos consumidores os servidores pré-configurados Traditional WebSphere e perfil Liberty. Ele é hospedado em convidados da máquina
virtual com acesso raiz para o sistema operacional guest. Quando você estiver criando seu serviço, escolha entre *Liberty*, *Traditional ND* ou *Traditional WebSphere*.

**Nota:** os consumidores são agora capazes de escolher entre a V8.5 e a V9.0 quando você cria uma nova instância do *Traditional ND* ou do *Traditional WebSphere*.

Você recebe uma experiência de administração do WebSphere familiar e tem acesso completo
ao sistema operacional subjacente. É possível reutilizar seus scripts existentes e fazer pequenos ajustes de sistema
necessários para trabalhar com suas estruturas próprias ou de terceiros. O Centro do administrador e os Consoles do administrador são fornecidos para administrar o serviço WebSphere Application Server Liberty, ND ou Traditional, assim como suas configurações do WebSphere no local.

O Plano do WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment consiste em um ambiente de célula do WebSphere Application Server Network Deployment com duas ou mais máquinas virtuais. A primeira máquina virtual contém o Deployment Manager e o IBM HTTP Server e as máquinas virtuais restantes contêm nós customizados (agentes de nó) federados para o Deployment Manager. Use seus scripts wsadmin existentes para criar sua configuração do WebSphere ou use
o Console administrativo do WebSphere para configurar manualmente o ambiente. Esses novos recursos permitem que os usuários configurem um ambiente em cluster, o que é um aspecto crítico de qualquer aplicativo corporativo de middleware. Os
clientes agora podem optar por agrupar uma topologia para balancear a carga de solicitações entre duas ou mais Instâncias.

O Plano do WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core inclui o uso de um Liberty Collective. O Liberty Collective é um domínio administrativo para um grupo de perfis Liberty (servidores) e consiste em duas ou mais máquinas virtuais. A
primeira máquina virtual contém o servidor Collective Controller liberty, que é um ponto de controle
para o Liberty Collective. Além do liberty collective, essa máquina virtual também
contém o IBM HTTP Server, que permite acesso aos aplicativos a partir de um navegador da web. As
máquinas virtuais restantes são os hosts coletivos nos quais os membros coletivos residem (servidores
do perfil liberty). O recurso Liberty Admin Center também é ativado no servidor liberty controller.

A figura a seguir mostra a arquitetura dos ambientes do WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment Cell e Liberty Collective.

Figura 1. Célula de implementação de rede e arquitetura Liberty Collective

![Figura1. Arquitetura da célula de implementação de rede e Liberty Collective](images/CellCollectiveDiagram.gif)

**Nota**: na *Figura 1* acima, o padrão que descreve a disposição do Gerenciador de Implementação ou do Controlador Coletivo com o IBM HTTP Server se
destina para propósitos de desenvolvimento e de testes. O WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} também lhe dá a liberdade de reconfigurar o software pré-instalado para atender às suas necessidades operacionais e do aplicativo de produção; tal como você faria no local. Além disso, para os requisitos de produção mais estritos, entre em contato com seu representante de vendas IBM que pode falar sobre nossa oferta do IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de locatário único, que oferece recursos de cálculo e de rede isolados.


## Ambiente Operacional
{: #operational_environment}

O IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} é um serviço que retorna guests
(máquinas virtuais) em um ambiente compartilhado para que os consumidores implementem aplicativos. Um VPN protege o serviço público de varreduras de portas genéricas e outros
ataques baseados em rede não solicitados. No entanto, é importante observar que a VPN de serviço que você usa para acessar
a sua instância de serviço pode ser compartilhada entre múltiplas organizações e usuários do
{{site.data.keyword.Bluemix_notm}}. As máquinas virtuais fornecem recursos de cálculo, de memória e de Entrada/Saída, os quais são provenientes de um conjunto compartilhado de recursos IaaS.

Como os recursos específicos de cálculo, de memória e de E/S são executados
por máquinas virtuais em um ambiente compartilhado, as configurações de serviço podem variar. As configurações para cada instância de serviço específica
podem ser visualizadas por meio dos portais e painéis de serviço do
IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}.

O IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} fornece instâncias da máquina virtual. Com essas instâncias, os clientes usam um portal simples para criar e gerenciar implementações corporativas do WebSphere Application Server de uma forma consistente e repetida com flexibilidade significativa para ajustar seus aplicativos. Os usuários podem começar a trabalhar em máquinas virtuais pré-configuradas do WebSphere Application Server Liberty, ND ou Traditional em um ambiente de nuvem hospedado. Os usuários podem migrar aplicativos existentes do WebSphere Application Server para o {{site.data.keyword.Bluemix_notm}} e assumir o controle total do sistema operacional e do middleware subjacentes.

## Estratégia de precificação
{: #pricing_strategy}

O IBM WebSphere Application Server for
{{site.data.keyword.Bluemix_notm}} fornece instâncias
dimensionadas para Camiseta para clientes com aplicativos de uso
intensivo de memória para dimensionar corretamente seu ambiente com máquinas virtuais maiores. Os clientes podem selecionar o tamanho do recurso específico de um componente provisionado do WebSphere Application Server ou de um único sistema com máquinas virtuais de até 32 GB de RAM.

As tabelas a seguir representam os preços dos planos do IBM
WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} a partir de 1 de abril de 2016 e são representados em dólares americanos (USD).

*Tabela 1. Plano do Liberty Core*

| **Camiseta** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Preço/H** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| P | 1 | 2 | 12 | US$ 0,21 |
| M | 2 | 4 | 25 | US$ 0,42 |
| G | 4 | 8 | 50 | US$ 0,84 |
| EG | 8 | 16 | 100 | US$ 1,68 |
| EEG | 16 | 32 | 200 | US$ 3,36 |

*Tabela 2. Plano base do WebSphere Application Server*

| **Camiseta** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Preço/H** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| P | 1 | 2 | 12 | US$ 0,30 |
| M | 2 | 4 | 25 | US$ 0,60 |
| G | 4 | 8 | 50 | US$ 1,20 |
| EG | 8 | 16 | 100 | US$ 2,40 |
| EEG | 16 | 32 | 200 | US$ 4,80 |

*Tabela 3. Plano do WebSphere Application Server ND*

| **Camiseta** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Preço/H** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| P | 1 | 2 | 12 | US$ 0,70 |
| M | 2 | 4 | 25 | US$ 1,40 |
| G | 4 | 8 | 50 | US$ 2,80 |
| EG | 8 | 16 | 100 | US$ 5,60 |
| EEG | 16 | 32 | 200 | US$ 11,20 |

<p></p>

O IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} é oferecido de acordo com a métrica de encargo a seguir:

*  *Hora por instância*: uma Instância é definida como acesso a uma configuração específica do serviço do IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}. Os clientes são cobrados por cada hora integral ou parcial de cada Instância do Serviço que é implementado durante o período de faturamento. Cada Hora da instância é faturada mensalmente e se uma instância for usada somente uma parte do mês, a taxa de uso será rateada.

Por exemplo, se você usar o Plano ND, uma Instância será equiparada a 1vCPU com 2 GB de RAM e 12 GB de HD. Portanto, se você escolher configurar sua Célula com um nó de Controle e oito nós Customizados, será cobrado por nove nós (instâncias).

**Nota**: o faturamento mínimo é configurado como 0,25 a hora da instância por nó Customizado ou host Liberty. No exemplo acima, um nó de Controle e um nó Customizado que esteja configurado para pelo menos 15 minutos seria equiparado a um encargo mínimo de (0,25 * n.º de instâncias).

**Nota**: em razão de uma quantia específica de recursos de cálculo, de memória e de E/S, os clientes são cobrados por instâncias acumuladas no estado INTERROMPIDO a uma taxa reduzida de 5%. Os clientes são gerenciados para um número fixo de instâncias INTERROMPIDAS com não mais de 10 endereços IP ou 64 GB de memória.

# rellinks
{: #rellinks}
## gerais
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentação do WebSphere Application Server V9](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
