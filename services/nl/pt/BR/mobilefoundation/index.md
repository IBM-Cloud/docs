---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

*Última atualização: 15 de junho de 2016*
{: .last-updated}

O {{site.data.keyword.mobilefoundation_long}} expede a configuração de um ambiente do {{site.data.keyword.mfp_full}} a partir do qual é possível desenvolver, testar e operar aplicativos móveis corporativos. O {{site.data.keyword.mobilefoundation_short}} está disponível em dois planos de serviços diferentes: Developer e Professional 1 Application.
{:shortdesc}

O plano Professional 1 Application permite que o servidor {{site.data.keyword.mobilefoundation_short}} seja implementado em um grupo de contêiner escalável. Usando o plano Professional 1 Application, um único aplicativo construído em qualquer uma ou em todas as plataformas operacionais suportadas, como Android, iOS, Windows ou web móvel, pode ser gerenciado. O plano Developer não suporta a implementação do {{site.data.keyword.mobilefoundation_short}} em um grupo de contêiner com mais de 1 nó. Esse plano é melhor adaptado para desenvolvimento e teste.

## Introdução ao plano {{site.data.keyword.mobilefoundation_short}}: Developer

Depois de criar uma instância do {{site.data.keyword.mobilefoundation_short}}: Developer, é possível iniciar a construção de seu canal móvel com apenas alguns cliques.

*	Para criar uma instância do servidor {{site.data.keyword.mobilefirst_notm}} com a configuração padrão, clique em **Iniciar servidor básico**.

  `A instância de servidor básico inclui um único
nó, 1 GB de memória e 64 GB de capacidade de armazenamento.`

* Para criar uma instância de servidor do {{site.data.keyword.mobilefirst_notm}} com configuração avançada para topologia, segurança e outra configuração do servidor, clique em **Iniciar servidor com configuração avançada**. Consulte [Instalando a configuração avançada](c_using_mfs_p1.html#using_mfs_advanced_p1), para obter mais informações.

## Introdução ao plano {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application

Depois de criar uma instância do serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, é possível iniciar a construção de seu canal móvel concluindo as etapas a seguir.

1.  Conecte-se ao serviço {{site.data.keyword.dashdbshort}}: Enterprise Transactional tradicional no {{site.data.keyword.Bluemix_notm}}.

    1.  Selecione o `Space` do {{site.data.keyword.Bluemix_notm}} no qual a instância de serviço {{site.data.keyword.dashdbshort_notm}} existe, na lista de espaços disponíveis na `Organization` atual.

    2.  Selecione o `Service Name` e as `Credentials` do {{site.data.keyword.dashdbshort_notm}} para se conectar à instância de serviço {{site.data.keyword.dashdbshort_notm}} existente.

    3.  Teste a conexão com a instância de serviço {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional selecionada, clicando em **Conexão de teste**.

    4.  Clique em **Incluir**, seguido de **Continuar**, na janela pop-up que solicita confirmação no serviço {{site.data.keyword.dashdbshort_notm}} selecionado. Essa ação cria as tabelas necessárias na instância de serviço de banco de dados {{site.data.keyword.dashdbshort_notm}} configurada.

2.  Crie e inicie o servidor.

    * Para criar uma instância do servidor {{site.data.keyword.mobilefirst_notm}} com a configuração padrão, clique em **Iniciar servidor básico**.

      `A instância de servidor básico inclui um único
nó, 1 GB de memória e 64 GB de capacidade de armazenamento.`

    * Para criar uma instância de servidor do {{site.data.keyword.mobilefirst_notm}} com configuração avançada para topologia, segurança e outra configuração do servidor, clique em **Iniciar servidor com configuração avançada**. Consulte [Instalando a configuração avançada](c_using_mfs_p2.html#using_mfs_advanced_p2), para obter mais informações.

Acesse [Usando o serviço Mobile Foundation para configurar o MobileFirst Server no IBM Containers](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/) para aprender mais sobre como iniciar o {{site.data.keyword.mobilefoundation_short}}.

# Links relacionados
{: #rellinks}

## Links relacionados
{: #general}

*	[Documentação do produto IBM MobileFirst Platform Foundation V8.0.0](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
