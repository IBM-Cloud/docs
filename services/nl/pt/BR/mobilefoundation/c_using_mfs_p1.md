---

copyright:
  years: 2016

---

#	Usando o {{site.data.keyword.mobilefoundation_short}}: Developer
{: #using_mobilefoundation_p1}

Depois de criar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Developer, execute as etapas a seguir para iniciar o serviço:

* Concorde com os termos de licença para o {{site.data.keyword.mfp_full_notm}} V8.0.0.0.

* Insira suas credenciais do {{site.data.keyword.Bluemix_notm}}. Isso autoriza o serviço a fazer mudanças no espaço do {{site.data.keyword.Bluemix_notm}} e criar o {{site.data.keyword.containerlong}} que hospeda o {{site.data.keyword.mobilefirst_notm}} Server.

Após alguns segundos, é possível acessar a página *Visão geral* no {{site.data.keyword.Bluemix_notm}}, que fornece os tutoriais e vídeos para ajudar a iniciar o serviço {{site.data.keyword.mobilefoundation_short}}.

## Iniciando o servidor {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Para iniciar o {{site.data.keyword.mfserver_short_notm}} com configurações padrão, clique em **Iniciar servidor básico**.

![Iniciar o servidor básico](images/start_basic_server.png "Figura 1. Iniciar o servidor básico")
{: screen}

Esta seleção provisiona um {{site.data.keyword.mfserver_long_notm}} com as configurações a seguir:
*	1 GB de memória e 64 GB de armazenamento. Esse tamanho é suficiente para desenvolvimento e atividades de
teste leve.

*	O *username* e a *password* são gerados automaticamente para
você. Você tem acesso a eles quando o servidor está funcionando.

O processo de fornecimento inicia. Esse processo leva aproximadamente 10 minutos e uma
janela de mensagem indica o progresso dessa operação. Quando completo, um painel é exibido
no qual é possível ver:
*	O status do servidor que está em execução (estado, tamanho, armazenamento).

*	A rota do servidor criada para você. Use essa rota para atingir o servidor móvel a partir da internet
pública. Seus aplicativos móveis usam essa rota para acessar o servidor.

*	Seu *nome do usuário* e *senha* para acessar o {{site.data.keyword.mfp_oc_short_notm}}. A *senha* fica oculta. Clique no ícone de olho pequeno para
visualizá-la.

*	Clique em **Ativar console** para ativar o {{site.data.keyword.mfp_oc_short_notm}}.

![Ativar console](images/launch_console.png "Figura 2. Ativar console")
{: screen}

Este console é executado dentro do contêiner. Com o console, é possível gerenciar os aplicativos móveis e dispositivos móveis, usar o servidor como um backend móvel, enviar notificações push e muito mais.

## Recriando o servidor {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p1}

*	Clique em **Recriar** para recriar o servidor.

![Recriar](images/recreate.png "Figura 3. Recriar")
{: screen}

* Esta ação para o servidor existente e o exclui. Todos os dados no servidor móvel são perdidos. Uma nova instância de servidor é criada. Esta ação
demora alguns minutos para ser concluída.

##	Definindo a configuração avançada
{: #using_mfs_advanced_p1}

Use **Iniciar servidor com a configuração avançada** na página *Visão geral* para criar o servidor com configurações avançadas ou customizadas. Também é possível
atualizar as definições do servidor para customizar a configuração do servidor clicando na
guia **Configuração**. O {{site.data.keyword.mobilefoundation_short}} fornece acesso a algumas configurações avançadas.

*	Na guia **Topologia**, é possível selecionar o tamanho da Topologia de seu contêiner. O servidor padrão de 1 GB é suficiente para desenvolvimento e teste moderado, mas talvez você precise mais, por exemplo, para executar o teste de carregamento.
  - Selecione o tamanho correto para seu servidor com base em sua necessidade.  


* **Nós** exibe o número de nós que são criados. Esse campo não é editável no {{site.data.keyword.mobilefoundation_short}}: Developer. É possível ver o número de nós obtidos em grupo de contêiner do {{site.data.keyword.IBM_notm}}. Os grupos de contêiner fornecem alta
disponibilidade e escalabilidade.

Consulte a [documentação do {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} para obter mais detalhes.
