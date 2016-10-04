---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Sobre o {{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
Última atualização: 12 de setembro de 2016
{: .last-updated}

O {{site.data.keyword.iotinsurance_full}} é uma instância de produção IoT integrada que coleta e analisa dados de contexto completos de segurados para fornecer avaliações de risco personalizadas, proteção em tempo real e reduções de custo de política.
{: shortdesc}

O {{site.data.keyword.iotinsurance_short}} fornece uma visualização de contexto completa dos ativos e da situação do segurado, incluindo informações, como localização, clima, tráfego e bem-estar geral. Uma análise detalhada dessas informações permite que o segurador forneça avaliação de risco personalizada e proteção em tempo real para o segurado. Os benefícios para o segurado incluem a prevenção de riscos na forma de alertas precoces, avisos personalizados e processamento e quitação aperfeiçoados de reclamações. Os benefícios para o segurador incluem satisfação do cliente, lealdade do cliente e redução de despesas usando prevenção de reclamações e automação de processamento.

## Fluxo do Processo
{: #processFlow}
O provedor de seguro possui uma instância dentro do broker de serviço do {{site.data.keyword.Bluemix_notm}}. Os clientes do segurador possuem sensores em suas casas, que são conectados à nuvem do provedor de sensor. A partir de seus dispositivos móveis, os proprietários de imóveis autorizam o serviço {{site.data.keyword.iotinsurance_short}} a receber dados do sensor do {{site.data.keyword.iotinsurance_short}}. O serviço {{site.data.keyword.iotinsurance_short}} conecta-se à nuvem do provedor de sensor e puxa dados de cada usuário e envia-os para o servidor IoT. Se o sensor mostrar que os parâmetros especificados nas proteções do segurador são atendidos na casa do cliente, notificações são enviadas para o painel do segurador e para o dispositivo do cliente.

## Componentes
{: #components}

### Painel do seguro
{: #insurance_dashboard}
O Painel do seguro fornece aos usuários da companhia de seguros, como agentes, uma visualização completa do que está acontecendo com os ativos segurados de seus clientes. Eles podem ver as proteções e os eventos em níveis de país, estado ou conta.

O painel de seguro de amostra é carregado com dados simulados para mostrar um exemplo do tipo de informações que podem ser coletadas e analisadas.

### App iniciador móvel
{: #mobileapp}
O app iniciador móvel é onde os segurados, como proprietários de imóveis, visualizam e respondem às informações que o {{site.data.keyword.iotinsurance_short}} envia dos sensores em suas casas.

Usando um dispositivo móvel, os proprietários de imóveis autorizam o serviço a conectar-se à nuvem do provedor de sensor para enviar e receber dados. Por exemplo, um proprietário de imóvel pode receber uma notificação no app iniciador móvel quando o sensor detecta um vazamento de água. Para obter mais informações, consulte [Instalando e conectando o app iniciador móvel](index.html#iot4i_mobile}).

### API REST
{: #rest_api}
A API REST é usada pelo app iniciador móvel, pelo painel de seguro, pelo mecanismo de proteção e pelo controlador de risco. Ela permite que os usuários conheçam as associações que existem entre os dispositivos, as proteções e as ações. Ao usar essa API, os programadores podem criar novos usuários, gerar dados do evento, criar e registrar novas proteções e buscar dados do evento.

A API que você acessa a partir do console de serviço é customizada para sua instância do {{site.data.keyword.iotinsurance_short}}.

Na página da API, é possível  
  - Visualizar todas as chamadas API disponíveis e a documentação associada.
  - Tentar chamadas API individuais.  Selecione uma chamada API para exibir todas as informações e, em seguida, clique em **Experimente!**.

Os exemplos de API estão disponíveis para ajudá-lo a iniciar a utilização de cenários comuns. Para obter mais informações, consulte [Exemplos de API do {{site.data.keyword.iotinsurance_short}}](https://github.ibm.com/Iot4i/iot4i-api-examples).

### Provedor em nuvem
{: #cloudprovider}
Os usuários devem autorizar o componente Transformer a acessar dados da nuvem do sensor e processar os dados registrados. A autorização é concedida usando o app iniciador móvel. Wink é o único fornecedor de nuvem suportado neste momento.

### Transformador
{: #transformer}
O Transformer solicita novas informações da API do servidor em nuvem e transforma-as para corresponder aos dados no {{site.data.keyword.iotinsurance_short}}. Os dados são então publicados para o restante da implementação do {{site.data.keyword.iotinsurance_short}} usar.

### Mecanismo de análise
{: #analytics_engine}
Com base nas informações armazenadas em um evento, o mecanismo de análise determinará se um risco, como um vazamento de água, ocorreu. Se um risco for identificado, ele será passado para o controlador de risco. O mecanismo de ação visualiza os dados no banco de dados para determinar a ação a ser tomada com base nas informações especificadas na proteção.

É possível criar novas proteções no JavaScript usando a API do {{site.data.keyword.iotinsurance_short}}.

### Shields
{: #shields}
Uma proteção é um item específico que um cliente adquire do provedor de seguro. Por exemplo, um proprietário de imóvel compra seguro para sua casa para protegê-la contra fogo, danos hídricos, assaltos e outros riscos. A solução {{site.data.keyword.iotinsurance_short}} fornece uma proteção integrada com relação à água. Os clientes são alertados e podem responder quando um evento que envolve água ameaça sua casa. Usando a API REST, os desenvolvedores podem incluir mais proteções.
As proteções são executadas no mecanismo de análise do {{site.data.keyword.iotinsurance_short}}. O mecanismo de análise identifica o tipo de risco (por exemplo, *Detecção de água*), a conta do usuário do sensor que enviou o risco e as proteções que estão associadas à conta. A ação pode ser executada com base nessas informações.
