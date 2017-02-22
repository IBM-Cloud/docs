---

copyright:
  years: 2016, 2017
lastupdated:  "2017-01-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

O {{site.data.keyword.mobilefoundation_long}} expede a configuração de um ambiente do {{site.data.keyword.mfp_full}} a partir do qual é possível desenvolver, testar e operar aplicativos móveis corporativos. O {{site.data.keyword.mobilefoundation_short}} está disponível em dois planos de serviços diferentes: Developer e Professional 1 Application.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Usando o plano Professional 1 Application, um único aplicativo desenvolvido em qualquer ou todas as plataformas operacionais suportadas, tais como Android, iOS, Windows ou web móvel, pode ser
gerenciado. O plano do Desenvolvedor <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> é mais adequado para desenvolvimento e teste.

## Introdução ao plano {{site.data.keyword.mobilefoundation_short}}: Developer

Depois de criar uma instância do {{site.data.keyword.mobilefoundation_short}}: Developer, é possível iniciar a construção de seu canal móvel com apenas alguns cliques.

*	Para criar uma instância do servidor {{site.data.keyword.mobilefirst_notm}} com a configuração padrão, clique em **Iniciar servidor básico**.

  `A instância do servidor básica inclui um único nó com 1 GB de memória.`

* Para criar uma instância de servidor do {{site.data.keyword.mobilefirst_notm}} com configuração avançada para topologia, segurança e outra configuração do servidor, clique em **Iniciar servidor com configuração avançada**. Consulte [Instalando a configuração avançada](c_using_mfs_p1.html#using_mfs_advanced_p1), para obter mais informações.

## Introdução ao plano {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application

Depois de criar uma instância do serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, é possível iniciar a construção de seu canal móvel concluindo as etapas a seguir.

1.  Conecte-se a um serviço {{site.data.keyword.dashdbshort}} for Transactions
existente no {{site.data.keyword.Bluemix_notm}}.

    1.  Selecione a {{site.data.keyword.Bluemix_notm}} `Organização` na qual a instância do serviço {{site.data.keyword.dashdbshort_notm}} existe.

    + Selecione o `Space` do
{{site.data.keyword.Bluemix_notm}}, no qual a instância de
serviço do {{site.data.keyword.dashdbshort_notm}} existe, na lista de espaços disponíveis na `Organization` atual.

    + Selecione o `Service Name` e as `Credentials` do {{site.data.keyword.dashdbshort_notm}} para se conectar à instância de serviço {{site.data.keyword.dashdbshort_notm}} existente.

    + Teste a conexão com a instância de serviço {{site.data.keyword.dashdbshort_notm}} for Transactions selecionada clicando em **Testar conexão**.

    + Clique em **Incluir**, seguido por **Continuar**
na janela pop-up que solicita confirmação no serviço {{site.data.keyword.dashdbshort_notm}}
for Transactions selecionado. Essa ação cria as tabelas necessárias na instância de serviço de banco de dados {{site.data.keyword.dashdbshort_notm}} configurada.

    **Nota:** após incluir uma conexão do
{{site.data.keyword.dashdbshort_notm}} na instância do
{{site.data.keyword.mobilefoundation_short}}, não será possível
mudá-la.

2.  Crie e inicie o servidor.

    * Para criar uma instância do servidor {{site.data.keyword.mobilefirst_notm}} com a configuração padrão, clique em **Iniciar servidor básico**.

      `A instância do servidor básica inclui um único nó com 1 GB de memória.`

    * Para criar uma instância de servidor do {{site.data.keyword.mobilefirst_notm}} com configuração avançada para topologia, segurança e outra configuração do servidor, clique em **Iniciar servidor com configuração avançada**. Consulte [Instalando a configuração avançada](c_using_mfs_p2.html#using_mfs_advanced_p2), para obter mais informações.

## Introdução ao plano {{site.data.keyword.mobilefoundation_short}}: Developer Pro

Após criar uma instância do serviço {{site.data.keyword.mobilefoundation_short}}:
Developer Pro, será possível iniciar a construção de seu canal móvel concluindo as etapas a seguir.

  1.  Conecte-se a um serviço {{site.data.keyword.dashdbshort}} for Transactions
existente no {{site.data.keyword.Bluemix_notm}}.

      1.  Selecione a {{site.data.keyword.Bluemix_notm}} `Organização` na qual a instância do serviço {{site.data.keyword.dashdbshort_notm}} existe.

      + Selecione o `Space` do
{{site.data.keyword.Bluemix_notm}}, no qual a instância de
serviço do {{site.data.keyword.dashdbshort_notm}} existe, na lista de espaços disponíveis na `Organization` atual.

      + Selecione o `Service Name` e as `Credentials` do {{site.data.keyword.dashdbshort_notm}} para se conectar à instância de serviço {{site.data.keyword.dashdbshort_notm}} existente.

      + Teste a conexão com a instância de serviço {{site.data.keyword.dashdbshort_notm}} for Transactions selecionada clicando em **Testar conexão**.

      + Clique em **Incluir**, seguido por **Continuar**
na janela pop-up que solicita confirmação no serviço {{site.data.keyword.dashdbshort_notm}}
for Transactions selecionado. Essa ação cria as tabelas necessárias na instância de serviço de banco de dados {{site.data.keyword.dashdbshort_notm}} configurada.

      **Nota:** após incluir uma conexão do
{{site.data.keyword.dashdbshort_notm}} na instância do
{{site.data.keyword.mobilefoundation_short}}, não será possível
mudá-la.

  2.  Crie e inicie o servidor.

      * Para criar uma instância do servidor {{site.data.keyword.mobilefirst_notm}} com a configuração padrão, clique em **Iniciar servidor básico**.

      * Esta seleção provisiona um {{site.data.keyword.mfserver_long_notm}} com as configurações a seguir:

          - Nó único com 1 GB de memória. Esse tamanho é suficiente para desenvolvimento, atividades de teste moderado e cargas de trabalho de produção em pequena escala.

          -	O `username` e a `password` são gerados automaticamente para você. Você tem acesso a eles quando o servidor está funcionando.

      * Para criar uma instância de servidor do {{site.data.keyword.mobilefirst_notm}} com configuração avançada para topologia, segurança e outra configuração do servidor, clique em **Iniciar servidor com configuração avançada**. Consulte [Instalando a configuração avançada](c_using_mfs_p3.html#using_mfs_advanced_p3), para obter mais informações.

## Introdução ao plano {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity

Após criar uma instância do serviço{{site.data.keyword.mobilefoundation_short}}:
Professional Per Capacity, será possível iniciar a construção de seu canal móvel concluindo as
etapas a seguir.

  1.  Conecte-se a um serviço {{site.data.keyword.dashdbshort}} for Transactions
existente no {{site.data.keyword.Bluemix_notm}}.

      1.  Selecione a {{site.data.keyword.Bluemix_notm}} `Organização` na qual a instância do serviço {{site.data.keyword.dashdbshort_notm}} existe.

      + Selecione o `Space` do
{{site.data.keyword.Bluemix_notm}}, no qual a instância de
serviço do {{site.data.keyword.dashdbshort_notm}} existe, na lista de espaços disponíveis na `Organization` atual.

      + Selecione o `Service Name` e as `Credentials` do {{site.data.keyword.dashdbshort_notm}} para se conectar à instância de serviço {{site.data.keyword.dashdbshort_notm}} existente.

      + Teste a conexão com a instância de serviço {{site.data.keyword.dashdbshort_notm}} for Transactions selecionada clicando em **Testar conexão**.

      + Clique em **Incluir**, seguido por **Continuar**
na janela pop-up que solicita confirmação no serviço {{site.data.keyword.dashdbshort_notm}}
for Transactions selecionado. Essa ação cria as tabelas necessárias na instância de serviço de banco de dados {{site.data.keyword.dashdbshort_notm}} configurada.

      **Nota:** após incluir uma conexão do
{{site.data.keyword.dashdbshort_notm}} na instância do
{{site.data.keyword.mobilefoundation_short}}, não será possível
mudá-la.

  2.  Crie e inicie o servidor.

      * Para criar uma instância do servidor {{site.data.keyword.mobilefirst_notm}} com a configuração padrão, clique em **Iniciar servidor básico**.

      * Esta seleção provisiona um {{site.data.keyword.mfserver_long_notm}} com as configurações a seguir:
          -  Dois nós com 1 GB de memória cada. Esse tamanho é bom para desenvolvimento, atividades de teste moderado e cargas de trabalho de produção em pequena escala.

          -	O `username` e a `password` são gerados automaticamente para você. Você tem acesso a eles quando o servidor está funcionando.

      * Para criar uma instância de servidor do {{site.data.keyword.mobilefirst_notm}} com configuração avançada para topologia, segurança e outra configuração do servidor, clique em **Iniciar servidor com configuração avançada**. Consulte [Instalando a configuração avançada](c_using_mfs_p4.html#using_mfs_advanced_p4), para obter mais informações.

Acesse [Usando o serviço Mobile Foundation para configurar o MobileFirst Server<!-- on IBM Containers--> ![Ícone de link externo](../../icons/launch-glyph.svg "Íconede link externo")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/ "Ícone de link externo"){: new_window} para saber mais sobre como iniciar com o {{site.data.keyword.mobilefoundation_short}}.


##  Limitações Conhecidas

* A interface com o usuário de serviço do {{site.data.keyword.mobilefoundation_short}} não usa o padrão específico de código de idioma selecionado pelo usuário para exibir números.


# Links relacionados
{: #rellinks}

## Links relacionados
{: #general}

*	[Documentação do produto IBM MobileFirst Platform Foundation V8.0.0 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html "Ícone de link externo"){: new_window}
*	[IBM MobileFirst Platform Developer Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobilefirstplatform.ibmcloud.com "Ícone de link externo"){: new_window}
