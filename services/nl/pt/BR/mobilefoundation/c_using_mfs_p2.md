---

copyright:
  years: 2016

---

#	Usando o {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application
{: #using_mobilefoundation_p2}


Depois de criar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, leia o procedimento a seguir para iniciar o serviço.

## Pré-requisitos
{: #prerequisites_p2}

Considere o seguinte antes de configurar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application.
* O {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application é suportado somente com os planos do {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (que suporta OLTP) {{site.data.keyword.Bluemix_notm}}.

* A instância de serviço {{site.data.keyword.dashdbshort_notm}} e suas credenciais devem estar disponíveis para que seja possível definir as configurações da instância de serviço {{site.data.keyword.mobilefoundation_short}}.

**Nota**: A instância de serviço {{site.data.keyword.dashdbshort_notm}} pode existir em qualquer *Espaço* dentro de sua *Organização* {{site.data.keyword.Bluemix_notm}}.  

## Configurando a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application
{: #configure_dashdb_p2}

###  Primeiras etapas
{: #firststeps_p2}

Depois de criar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, execute as etapas a seguir para iniciar o serviço:

* Concorde com os termos de licença para o {{site.data.keyword.mfp_full_notm}} V8.0.0.0.

* Insira suas credenciais do {{site.data.keyword.Bluemix_notm}}. Isso autoriza o serviço a fazer mudanças no espaço do {{site.data.keyword.Bluemix_notm}} e criar o {{site.data.keyword.containerlong}} que hospeda o {{site.data.keyword.mobilefirst_notm}} Server.


### Configurando a conexão para a instância de serviço {{site.data.keyword.dashdbshort_notm}}
{: #connect_dashdb_p2}

Após a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application ser criada, você verá a página *Visão geral* na qual precisará especificar informações de conexão para a instância de serviço {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional.

* Especifique a **Organização** e o **Espaço** do {{site.data.keyword.Bluemix_notm}} nos quais a instância de serviço {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional existe.
* Escolha o **Nome do serviço** da instância de serviço {{site.data.keyword.dashdbshort_notm}} que você deseja usar com sua instância de serviço {{site.data.keyword.mobilefoundation_short}}, na lista suspensa, se tiver mais de uma instância de serviço {{site.data.keyword.dashdbshort_notm}} criada.
* Escolha as **Credenciais** para a instância de serviço {{site.data.keyword.dashdbshort_notm}} selecionada.

* Clique em **Conexão de teste** para verificar se a instância de serviço {{site.data.keyword.dashdbshort_notm}} está disponível, clique em **Salvar**.

**Nota**: não será possível mudar essa instância de serviço {{site.data.keyword.dashdbshort_notm}} que está configurada para ser usada por sua instância de serviço {{site.data.keyword.mobilefoundation_short}}. No entanto, será possível usar a mesma instância de serviço {{site.data.keyword.dashdbshort_notm}} em múltiplas instâncias de serviço {{site.data.keyword.mobilefoundation_short}}, uma vez que cada instância de serviço {{site.data.keyword.mobilefoundation_short}} criará seu próprio esquema na instância de serviço {{site.data.keyword.dashdbshort_notm}} selecionada.

* Após alguns segundos, é possível acessar a página *Visão geral* que fornece os tutoriais e vídeos para ajudar a iniciar o serviço {{site.data.keyword.mobilefoundation_short}}.

### Iniciando o Servidor {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p2}

* Para iniciar o {{site.data.keyword.mfserver_short_notm}}, com as configurações padrão, clique em **Iniciar servidor básico**.

![Iniciar o servidor básico](images/start_basic_server.png "Figura 1. Iniciar o servidor básico")
{: screen}
* Esta seleção provisiona um {{site.data.keyword.mfserver_long_notm}} com as configurações a seguir:
    -  1 GB de memória e 64 GB de armazenamento. Este tamanho é suficiente para atividades de desenvolvimento e de teste moderado.

    -	O *username* e a *password* são gerados automaticamente para
você. Você tem acesso a eles quando o servidor está funcionando.

O processo de fornecimento do servidor inicia. Esse processo leva aproximadamente 10 minutos e uma
janela de mensagem indica o progresso dessa operação. Quando completo, um painel é exibido
no qual é possível ver:

  -	O status do servidor que está em execução (estado, tamanho, armazenamento).

  -	A rota do servidor criada para você. Use essa rota para atingir o servidor móvel a partir da internet
pública. Seus aplicativos móveis usam essa rota para acessar o servidor.

  -	Seu *nome do usuário* e *senha* para acessar o {{site.data.keyword.mfp_oc_short_notm}}. A *senha* fica oculta. Clique no ícone de olho pequeno para
visualizá-la.

*	Clique em **Ativar console** para abrir o {{site.data.keyword.mfp_oc_short_notm}}.

![Ativar console](images/launch_console.png "Figura 2. Ativar console")
{: screen}

Este console é executado dentro do contêiner. Com o console, é possível gerenciar os aplicativos móveis e dispositivos móveis, usar o servidor como um backend móvel, enviar notificações push e muito mais.

### Recriando o servidor {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p2}

*	Clique em **Recriar** para recriar o servidor.

![Recriar](images/recreate.png "Figura 3. Recriar")
{: screen}

* Esta ação para o servidor existente e o exclui. Uma nova instância de servidor é criada. Esta ação
demora alguns minutos para ser concluída.

**Nota**: todos os dados de sua instância de servidor anterior, incluindo informações sobre os aplicativos e adaptadores, são persistidos na instância de serviço {{site.data.keyword.dashdbshort_notm}} configurada, isso estará disponível para uso após o servidor ser recriado.

##	Definindo a configuração avançada
{: #using_mfs_advanced_p2}

Use **Iniciar servidor com a configuração avançada** na página *Visão geral* para criar o servidor com configurações avançadas ou customizadas. Também é possível
atualizar as definições do servidor para customizar a configuração do servidor clicando na
guia **Configuração**. O {{site.data.keyword.mobilefoundation_short}} fornece acesso a algumas configurações avançadas.

*	Na guia **Topologia**, é possível selecionar o tamanho da Topologia de seu contêiner. O servidor padrão de 1 GB é suficiente para desenvolvimento e teste leve, mas talvez você precise mais, por exemplo, para executar o teste de carregamento.
  - Selecione o tamanho correto para seu servidor com base em sua necessidade.

  - **Nós** exibe o número de nós que são criados.
      - É possível configurar o número de nós mínimo e máximo requeridos nos grupos de contêiner do {{site.data.keyword.IBM_notm}}. Os grupos de contêiner fornecem alta
disponibilidade e escalabilidade.

      - O server farm do {{site.data.keyword.mobilefirst}} pode ser criado configurando o número de nós aqui.

Consulte a [documentação do {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} para obter mais detalhes.
