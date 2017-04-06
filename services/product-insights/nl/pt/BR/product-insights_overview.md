---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Sobre o IBM {{site.data.keyword.product-insights_short}}
{: #about_product-insights}

{{site.data.keyword.product-insights_full}} é um serviço IBM Bluemix, que faz parte do IBM Connect para Cloud. Ele conecta seus produtos de software IBM no local ao seu serviço do {{site.data.keyword.product-insights_short}} e fornece insights ao seu inventário em execução e às métricas de uso de tempo de execução.

{:shortdesc}

O serviço {{site.data.keyword.product-insights_short}} é um ponto de entrada, e mais funções podem ser incluídas no futuro.

O {{site.data.keyword.product-insights_short}} fornece os seguintes recursos:

* Registro de seus produtos de software IBM no local com a IBM, especificamente com um serviço Bluemix.
* Coleta de dados para produtos no local conectados e dados de uso associados.
* Painel para dados de uso de tempo de execução para fornecer insights reais sobre o uso do produto e a carga de trabalho.


Para usar os recursos do {{site.data.keyword.product-insights_full}}, conclua as etapas a seguir:

1. Crie pelo menos um serviço no Bluemix para {{site.data.keyword.product-insights_short}}.
1. Faça upgrade de seus produtos de software IBM no local para os níveis de liberação necessários e inclua o código de ativação para cada instalação do produto. 
1. Configure a instalação de software com as credenciais do {{site.data.keyword.bluemix_short}} para sua instância de serviço do {{site.data.keyword.product-insights_short}}. Todos os seus dados são armazenados com segurança com essas credenciais. Os dados estão disponíveis apenas para os indivíduos com as permissões adequadas ao serviço.



## Como ele funciona
{: #product-insights_howitworks}
O serviço {{site.data.keyword.product-insights_full}} se integra aos seus produtos de software IBM no local para reunir e exibir informações do produto de tempo de execução e métricas de uso. Inicialmente, um subconjunto de produtos de software IBM é ativado para se integrar a este serviço. Quando registrados e conectados, os produtos de software no local enviam periodicamente informações de inicialização e uso. As informações são armazenadas em relação a essa instância de serviço por meio das credenciais configuradas. É possível usar o painel de instância de serviço para visualizar as informações no Bluemix.

A solução {{site.data.keyword.product-insights_short}} inclui vários componentes, conforme mostrado no gráfico a seguir:

![{{site.data.keyword.product-insights_full}} arquitetura](images/architecture_product-insights.png "{{site.data.keyword.product-insights_full}} architecture").  


## Organizações e espaços
{: #product-insights_orgs}
O serviço {{site.data.keyword.product-insights_full}} está associado a uma única organização e espaço do Bluemix e tem credenciais exclusivas. Deve-se configurar pelo menos uma organização e espaço do Bluemix. Se desejar separar os dados, por exemplo, para limitar o acesso a indivíduos específicos, você poderá criar vários espaços dentro de uma organização com uma instância de serviço em cada espaço. Cada instância de serviço tem credenciais exclusivas que você precisa fornecer a seus produtos de software IBM.

As informações para os produtos que são configurados com um conjunto de credenciais são visíveis apenas dentro do serviço com essas credenciais. Vários serviços podem ser criados para separar os dados se necessário, cada um com credenciais exclusivas.


## Painel de serviço
{: #service_dashboard}
Depois de criar sua instância de serviço, você é direcionado ao painel de serviço. Você sempre pode retornar ao painel de serviço clicando no ícone de serviço no painel da organização. No painel de serviço, é possível acessar os seguintes itens:

* A documentação de Introdução
* As credenciais de serviço necessárias para conectar seus produtos no local
* Um inventário de produtos suportados e todas as instâncias de tempo de execução registradas na instância de serviço do {{site.data.keyword.product-insights_short}}
* Informações de uso para instâncias de tempo de execução conectadas
* Informações do produto e do ambiente para instâncias de tempo de execução conectadas

Se não houver produtos listados na guia Gerenciar, clique em **Registrar um produto** para visualizar uma lista de produtos suportados e acessar detalhes específicos sobre como conectar instâncias do produto.
![Painel de serviço sem nenhum produto registrado](images/NoRegisteredProducts.jpg "Service dashboard with no registered products")

## Registrar um produto
{: #product-insights_register}
Na guia **Gerenciar**, clique em **Registrar um produto** para visualizar uma lista de produtos suportados. Role para seu produto ou use um campo de procura para filtrar a lista de produtos.
![Lista de produtos suportados filtrada usando a sequência de procura](images/products-filtered.png "Filtered list of products available to be registered")

Para visualizar instruções sobre como registrar uma instância de um produto, selecione-o na lista.

Ao conectar uma instância do produto ao serviço do {{site.data.keyword.product-insights_short}}, ele é exibido na guia **Gerenciar** do painel. Um painel pode listar várias instâncias de produtos conectadas em diferentes produtos.

## Inventário do produto
{: #product-insights_products}
Depois de ativar as instâncias do produto para enviar dados para o {{site.data.keyword.product-insights_short}}, é possível visualizar seu inventário selecionando **Gerenciar** no painel de serviço.

![Painel de serviço com produtos e instâncias do produto](images/productinstances.png "Service dashboard with products and product instances") 

Para o {{site.data.keyword.product-insights_short}}, um produto é diferente de uma instância do produto. Um produto tem um nome de produto, como IBM MQ ou IBM WebSphere Application Server Liberty Network Deployment. Uma instância de produto é usada para representar um produto depois que ele é instalado e está em execução. Alguns produtos têm várias instâncias que são executadas na mesma instalação do produto. Por exemplo, o WebSphere Application Server Liberty Network Deployment pode executar vários servidores de aplicativos que são criados em uma única instalação do produto.

No painel de serviço, os nomes dos produtos registrados são mostrados na opção *Visualizar tudo* na área de janela **Produtos**. Instâncias conectadas são listadas na área de janela **Instâncias**. Esta área de janela contém instâncias dos produtos que são selecionados na área de janela **Produtos**. No exemplo a seguir, todas as instâncias do produto são mostradas porque a opção *Visualizar tudo* é selecionada na área de janela Produtos. Este exemplo mostra seis produtos, alguns com várias instâncias conectadas. É possível filtrar a lista de instâncias usando o campo **Procurar Instâncias** ou selecionando uma entrada do produto. Para visualizar detalhes para uma instância do produto, selecione sua entrada na área de janela **Instâncias**.

A lista de instâncias do produto que são exibidas é filtrada conforme você navega. Para auxiliar a navegação, o caminho navegado para uma instância selecionada é exibido.

![Painel de serviço](images/products.png "Service dashboard") 



## Informações da instância do produto
{: #product-insights_productinstances}
Quando uma instância do produto é selecionada, a área de janela **Detalhes da instância** é preenchida. A área de janela mostra dados de uso, detalhes do produto e recomendações para a instância do produto por meio de uma guia **Advisor**.


## Informações de uso
{: #product-insights_usage}
As informações de uso são mostradas na guia **Uso**. Use as duas listas suspensas para selecionar a métrica a exibir (se a instância do produto enviar mais de uma métrica) e o período de tempo a ser exibido.

Se a instância do produto enviar mais de uma métrica, use a primeira lista suspensa para selecionar qual métrica exibir. Na segunda lista suspensa, selecione o período de tempo a exibir. As opções para o período de tempo para as seções são Últimas 24 horas, 1 semana, 1 mês, 6 meses, 1 ano.

A primeira seção mostra a média máxima, média, média mínima e o total dos valores da métrica sobre o período de tempo selecionado. A segunda seção mostra um gráfico dos valores dentro do período de tempo com o período do eixo X, que muda com base no período de tempo selecionado. Por exemplo, Últimas 24 horas mostra pontos gráficos para cada hora, enquanto a exibição de 1 semana mostra pontos gráficos para cada dia dentro dessa semana). A seção final mostra o máximo, médio e mínimo para o ponto gráfico selecionado. Para ver os valores para outro ponto no gráfico, arraste a barra de tempo para uma nova posição.

Uma mensagem será exibida se não houver nenhum dado para esse período de tempo. Por exemplo, uma instância parada não forneceria dados e nenhum dado será mostrado para o período de tempo em que estava parada. Outros períodos de tempo podem ter uso a exibir. Mude o período de tempo na lista suspensa para ver outros períodos de tempo.

A guia **Detalhes** mostra informações da instância do produto, que podem incluir os seguintes itens:

* O nome e a versão do produto
* O local em que o produto está instalado, incluindo o nome do host e o diretório
* A última vez em que a instância enviou informações sobre a inicialização
* O identificador da instância se o produto puder ter várias instâncias em um único diretório

![Detalhes da instância do produto](images/instancedetail.png "Product instance details") 

A instância do produto também fornece as seguintes informações opcionais:

* Uma lista de APARs instaladas. 
* O sistema operacional e sua versão, que são mostrados na guia **Ambiente**.
![Detalhes da instância do produto - guia Ambiente](images/instancedetails-env.png "Product instance details - Environment tab")
* Componentes ou recursos instalados, que são mostrados na guia **Componentes**. O exemplo não mostra a guia **Componentes** porque a instância do IBM Product XYZ não fornece nenhuma informação de componente adicional.
![Detalhes da instância do produto - guia Componente](images/instancedetails-comps.png "Product instance details - Component tab")
* O identificador exclusivo para a instância do produto, que é uma combinação do nome do host, diretório e identificador da instância.

 


## Procurando 
{: #product-insights_search}
A área de janela **Instância do produto** fornece um recurso de procura básica para filtrar a lista de produtos. No campo de procura, digite a sequência que deseja usar para a procura. A procura pode ser feita apenas para dados de instância do produto (ou seja, as informações na guia **Detalhes**).



<!-- If your service doc doesn't have a troubleshooting topic or section, you can add the following to your About: -->
<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->
## Obtendo ajuda para o {{site.data.keyword.product-insights_short}}
{: #gettinghelp}

Informações detalhadas sobre como criar um serviço, obter as atualizações para os produtos de software IBM ativados e as etapas de instalação e configuração são localizadas na [{{site.data.keyword.product-insights_full}} Comunidade Técnica](https://developer.ibm.com/product-insights/). Se você tiver problemas ou dúvidas quando estiver usando o {{site.data.keyword.product-insights_short}}, visualize ou poste as dúvidas na seção Fóruns da Comunidade. Estas dúvidas são respondidas pela equipe de programas de desenvolvimento e do cliente.

É possível também usar os fóruns Stack Overflow e IBM DeveloperWorks dw Answers para visualizar ou postar dúvidas. Para dúvidas sobre o serviço e instruções de início, use o IBM developerWorks dW Answers. Quando postar uma dúvida em qualquer um desses dois fóruns, aplique as seguintes regras de tag para que as equipes de desenvolvimento do Bluemix possam ver facilmente sua dúvida.

* Clique para postar em [Stack Overflow](http://stackoverflow.com/search?q=hybrid-connect+ibm-bluemix){:new_window}, identifique sua dúvida com "ibm-bluemix" e "productinsights".
* Clique para postar em [IBM developerWorks dW Answers](https://developer.ibm.com/answers/smartspace/productinsights/){:new_window}, identifique suas dúvidas com "productinsights" ou "hybridconnect".

Para obter mais informações sobre como usar os fóruns, consulte o tópico [Obtendo ajuda](https://www.{DomainName}/docs/support/index.html#getting-help).
