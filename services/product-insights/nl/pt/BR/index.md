---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Introdução ao {{site.data.keyword.product-insights_short}}
{: #product-insights}

O {{site.data.keyword.product-insights_full}} se conecta a produtos de software IBM no local para construir um inventário de produto cruzado e fornecer insights sobre métricas de uso de produto.

{:shortdesc}

O serviço {{site.data.keyword.product-insights_short}} é executado dentro do IBM Bluemix e recebe informações dos produtos de software IBM ativados no local. Essas informações são então mostradas no painel da instância de serviço. Para usar o serviço, você deve ter uma conta do Bluemix e criar o serviço em uma organização e espaço. As informações do produto e de uso para seus produtos ativados no local são armazenadas com segurança e visualizadas dentro do escopo ou contexto desse serviço exclusivo. 

Dica: para simplificar, é possível usar inicialmente uma única instância de serviço.

Para iniciar o {{site.data.keyword.product-insights_short}}, conclua as etapas a seguir:

1.  Na guia **Gerenciar**, clique no botão **Registrar um produto** para visualizar uma lista de produtos suportados e o nível de versão necessário. São fornecidas instruções para cada tipo de produto, para que seja possível se conectar a instâncias do produto no local para o serviço {{site.data.keyword.product-insights_short}}. Se necessário, atualize seus produtos de software IBM no local, ativados para o nível mínimo de pré-requisito. Para um produto que requer um nível mínimo suportado, instale o fix pack ou a correção temporária para permitir a integração com o {{site.data.keyword.product-insights_short}}. 
2.  Conecte seus produtos de software IBM no local, ativados no serviço do {{site.data.keyword.product-insights_short}}. Como parte do processo de configuração para cada produto, você precisa das credenciais de serviço (ou seja, apikey e apihost). É possível localizar as credenciais de serviço na guia **Credenciais de Serviço** do seu painel de serviço. 
3.  Depois de ativar e conectar cada instância do produto, pode ser necessário iniciar ou reiniciar os produtos ou as instâncias do produto para que forneçam informações do produto e de uso para o serviço do {{site.data.keyword.product-insights_short}}. 

Para obter detalhes sobre a ativação de produtos, o nível mínimo de suporte necessário para cada produto e o modo de ativar cada produto para integração com o {{site.data.keyword.product-insights_short}}, faça parte da {{site.data.keyword.product-insights_full}} [Comunidade Técnica](https://developer.ibm.com/product-insights/).

É possível visualizar seu inventário selecionando **Gerenciar** no painel de serviço.  

* No painel de serviço, os nomes dos produtos que foram conectados são listados na área de janela **Produtos**. 
* Para mostrar todas as instâncias do produto, selecione **Visualizar tudo**. Para mostrar as instâncias para um produto, selecione esse produto na área de janela **Produtos** e elas serão exibidas na área de janela **Instâncias**.
* Para mostrar os detalhes de uma única instância do produto, selecione a instância do produto na área de janela **Instâncias**. A área de janela **Detalhes** é, então, preenchida. A área de janela **Detalhes** mostra detalhes da instância do produto e as informações de uso que foram enviadas da instância.
* A guia **Uso** mostra as informações de uso do produto em formato gráfico. Dependendo do produto, é possível especificar o tipo de informações que você deseja visualizar e o período de amostragem.
* A guia **Detalhes** mostra informações da instância do produto; incluindo informações do produto, do ambiente e do componente.
* A guia **Advisor**, em sua guia **Serviços**, fornece detalhes sobre serviços adicionais que podem ser úteis em relação à instância do produto atual. Na guia **Atualizações**, fornece informações sobre o nível de versão da instância do produto e sua moeda.










