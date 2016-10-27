---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando conectividade móvel e segurança
{: #iot4e_configureMCA}

*Última atualização: 19 de setembro de 2016*
{: .last-updated}

Ative comunicações móveis e segurança configurando {{site.data.keyword.amafull}}. Essa tarefa é necessária para usar o aplicativo móvel de amostra e só precisa ser executada uma vez.
{:shortdesc}

## Antes de começar

Antes de iniciar, você deve concluir as seguintes tarefas:
  - Implemente uma instância do iniciador do {{site.data.keyword.iotelectronics}} em sua organização do {{site.data.keyword.Bluemix_notm}}. Implementar uma instância do iniciador
automaticamente implementa os aplicativos e serviços de componente, incluindo {{site.data.keyword.amafull}}.

  - Como o processo de configuração varia um pouco dependendo de qual versão do console do {{site.data.keyword.Bluemix_notm}} é usada, você deverá ler as instruções para a versão
apropriada.

  É possível determinar qual versão está sendo usada procurando as opções a seguir:
    - [Novo {{site.data.keyword.Bluemix_notm}}](#configMCAnew). Se você estiver usando a experiência do {{site.data.keyword.Bluemix_notm}} Novo, a opção
**Acessar a experiência clássica** aparecerá na seção de título do painel.
    - [{{site.data.keyword.Bluemix_notm}}](#configMCAclassic) Clássico. Se você estiver usando a experiência do {{site.data.keyword.Bluemix_notm}} Clássico, a opção
**Tente o Novo Bluemix** aparecerá na seção de título.

## Configurando {{site.data.keyword.amashort}} na experiência do {{site.data.keyword.Bluemix_notm}} Novo
{: #configMCAnew}

  1. Se você acabou de implementar o iniciador do {{site.data.keyword.iotelectronics}}, a guia Introdução do aplicativo iniciador será exibida e você deverá continuar para a próxima etapa
dessas instruções. Se o aplicativo iniciador não for exibido, abra o seu painel do {{site.data.keyword.Bluemix_notm}} e inicie o seu aplicativo iniciador {{site.data.keyword.iotelectronics}}
clicando no tile do aplicativo iniciador.

    ![{{site.data.keyword.iotelectronics}} no painel, Nova
experiência](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} in the dashboard, New Experience")

  2. Na guia **Conexões**, clique no serviço do {{site.data.keyword.amashort}} para abri-lo.

    ![Como localizar {{site.data.keyword.amashort}}.](images/IoT4E_Connections.png "{{site.data.keyword.iotelectronics}} connections")

  3. Na página **Configurar autenticação**, localize a URL de seu aplicativo iniciador {{site.data.keyword.iotelectronics}} clicando em **Opções
móveis**. Copie a URL que está localizada no campo **Rota**.

    ![Opções móveis do {{site.data.keyword.amashort}}](images/MCA_config_mobileoptions.png "{{site.data.keyword.amashort}} Mobile options")  

  4. Na página **Seção customizada da **Autenticação de configuração**, clique em **Configurar**.

       ![Configurar {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "{{site.data.keyword.amashort}} Setup Authentication page")  

  5. Insira as credenciais de autenticação a seguir e, em seguida, clique em **Salvar**:
    - **Nome da região**: insira **myRealm**.
    - **URL do provedor de identidade customizado**: insira a URL que você copiou anteriormente para identificar
o seu aplicativo iniciador {{site.data.keyword.iotelectronics}} no formato a seguir:
**https://<*myIoT4eStarterApp*>.mybluemix.net**
    - **URIs de redirecionamento de seu aplicativo da web**: deixe esse campo em branco.

      ![{{site.data.keyword.amashort}} Entrada de autenticação customizada.](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} Custom Authenticationentry")  


  6. Retorne à guia Conexões do console do iniciador do {{site.data.keyword.iotelectronics}} clicando no nome do aplicativo iniciador, que está localizado na seção de título.

   ![ trilha de navegação do {{site.data.keyword.amashort}}.](images/MCA_breadcrumb.png "{{site.data.keyword.amashort}} breadcrumb")

## Configurando {{site.data.keyword.amashort}} na experiência do {{site.data.keyword.Bluemix_notm}} Clássico
{: #configMCAclassic}

1. Em seu painel do {{site.data.keyword.Bluemix_notm}}, inicie o seu aplicativo iniciador {{site.data.keyword.iotelectronics}} clicando no tile do aplicativo iniciador.

    ![{{site.data.keyword.iotelectronics}} no painel, Clássico.](images/IoT4E_bm_dashboard_c.png "{{site.data.keyword.iotelectronics}} in the dashboard, Classic")

2. Em sua instância do {{site.data.keyword.iotelectronics}}, clique no serviço do {{site.data.keyword.amashort}} para abri-lo.   

  ![Como localizar {{site.data.keyword.amashort}}.](images/IoT4E_Connections_c.png "{{site.data.keyword.iotelectronics}} connections")

2. Na página **Configurar autenticação**, localize a URL de seu aplicativo iniciador {{site.data.keyword.iotelectronics}} clicando em **Opções móveis**. 
Copie a URL que está localizada no campo **Rota**.

  ![Opções móveis do {{site.data.keyword.amashort}}](images/MCA_config_mobileoptions.png "{{site.data.keyword.amashort}} Mobile options")  

3. Na página **Seção customizada da **Autenticação de configuração**, clique em **Configurar**.

 ![Configurar {{site.data.keyword.amashort}}.](images/MCA_config_pg.png "{{site.data.keyword.amashort}} Setup Authentication page")  

4. Insira as credenciais de autenticação a seguir e, em seguida, clique em **Salvar**:
   - **Nome da região**: insira **myRealm**.
   - **URL do provedor de identidade customizado**: insira a URL que você copiou anteriormente para identificar o seu aplicativo iniciador
{{site.data.keyword.iotelectronics}} no formato a seguir: **https://<*myIoT4eStarterApp*>.mybluemix.net**
   - **URIs de redirecionamento de seu aplicativo da web**: deixe esse campo em branco.

    ![{{site.data.keyword.amashort}} Entrada de autenticação customizada.](images/MCA_config_pg2.png "{{site.data.keyword.amashort}} Custom Authenticationentry")  


5. Retorne à guia Conexões do console do iniciador do {{site.data.keyword.iotelectronics}}, como segue:
  1. Exiba o menu, clicando nas setas duplas ao lado da opção **Voltar para o painel** na seção de título.
  2. Clique em **Visão geral** para retornar para o console do iniciador.  

    ![ trilha de navegação do {{site.data.keyword.amashort}}.](images/MCA_breadcrumb_c.png "{{site.data.keyword.amashort}} breadcrumb")
