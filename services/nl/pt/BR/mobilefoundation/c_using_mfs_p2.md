---

copyright:
  years: 2016

---

#	Usando o plano Professional 1 Application
{: #using_mobilefoundation_p2}

*Última atualização: 15 de junho de 2016*
{: .last-updated}

Depois de criar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, leia o procedimento a seguir para iniciar o serviço.

## Pré-requisitos
{: #prerequisites_p2}

Considere o seguinte antes de configurar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application.
* O {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application é suportado somente com os planos do {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (que suporta OLTP) {{site.data.keyword.Bluemix_notm}}.

* A instância de serviço {{site.data.keyword.dashdbshort_notm}} e suas credenciais devem estar disponíveis para que seja possível definir as configurações da instância de serviço {{site.data.keyword.mobilefoundation_short}}.

**Nota**: a instância de serviço {{site.data.keyword.dashdbshort_notm}} pode existir em qualquer `Space` de sua `Organization` {{site.data.keyword.Bluemix_notm}}. Se você optar por implementar o serviço {{site.data.keyword.mobilefoundation_short}} em um `Space` do {{site.data.keyword.Bluemix_notm}} diferente daquele no qual o serviço {{site.data.keyword.dashdbshort_notm}} existe, deverá assegurar-se de que tenha as permissões para acessar o serviço {{site.data.keyword.dashdbshort_notm}}.


## Incluindo a conexão com o banco de dados
{: #configure_dashdb_p2}

###  Primeiras etapas
{: #firststeps_p2}

Depois de criar a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, concorde com os termos de licença do {{site.data.keyword.mfp_full_notm}} V8.0, para iniciar.

### Configurando a conexão para a instância de serviço {{site.data.keyword.dashdbshort_notm}}
{: #connect_dashdb_p2}

Após a instância de serviço {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application ser criada, você verá a página *Visão geral* na qual precisará especificar informações de conexão para a instância de serviço {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional.

1.  Selecione o `Space` do {{site.data.keyword.Bluemix_notm}} no qual a instância de serviço {{site.data.keyword.dashdbshort_notm}} existe, na lista de espaços disponíveis na `Organization` atual.

+ Selecione o `Service Name` e as `Credentials` do {{site.data.keyword.dashdbshort_notm}} para se conectar à instância de serviço {{site.data.keyword.dashdbshort_notm}} existente.

+  Teste a conexão para a instância de serviço {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional especificada.

+  Clique em **Continuar**. Essa ação cria as tabelas necessárias na instância de serviço de banco de dados {{site.data.keyword.dashdbshort_notm}} configurada.

**Nota**: não é possível mudar a instância de serviço {{site.data.keyword.dashdbshort_notm}} que está configurada para ser usada por sua instância de serviço {{site.data.keyword.mobilefoundation_short}}. No entanto, é possível usar a mesma instância de serviço {{site.data.keyword.dashdbshort_notm}} em múltiplas instâncias de serviço {{site.data.keyword.mobilefoundation_short}}, uma vez que cada instância de serviço {{site.data.keyword.mobilefoundation_short}} cria seu próprio esquema na instância de serviço {{site.data.keyword.dashdbshort_notm}} selecionada.

* Em alguns segundos, é possível acessar a página `Overview` que fornece tutoriais e vídeos para ajudar a iniciar o serviço {{site.data.keyword.mobilefoundation_short}}.

## Iniciando o servidor {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p2}

* Para iniciar o {{site.data.keyword.mfserver_short_notm}}, com as configurações padrão, clique em **Iniciar servidor básico**.

* Esta seleção provisiona um {{site.data.keyword.mfserver_long_notm}} com as configurações a seguir:
    -  1 GB de memória e 64 GB de armazenamento. Este tamanho é suficiente para atividades de desenvolvimento e de teste moderado.

    -	O `username` e a `password` são gerados automaticamente para
você. Você tem acesso a eles quando o servidor está funcionando.

O processo de fornecimento do servidor inicia. Esse processo leva aproximadamente 10 minutos e uma
janela de mensagem indica o progresso dessa operação. Quando completo, um painel é exibido
no qual é possível ver:

  -	O status do servidor que está em execução (estado, tamanho, armazenamento).

  -	A rota do servidor criada para você. Use essa rota para atingir o servidor móvel a partir da internet
pública. Seus aplicativos móveis usam essa rota para acessar o servidor.

  -	Seu `nome do usuário`` e `senha` para acessar o {{site.data.keyword.mfp_oc_short_notm}}. A `password fica oculta. Clique em **Mostrar senha** para visualizá-la.

*	Clique em **Ativar console** para abrir o {{site.data.keyword.mfp_oc_short_notm}}.


Este console é executado dentro do contêiner. Com o console, é possível gerenciar os aplicativos móveis e dispositivos móveis, usar o servidor como um backend móvel, enviar notificações push e muito mais.

## Recriando o servidor {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p2}

*	Clique em **Recriar** para recriar o servidor.

* Esta ação para o servidor existente e o exclui. Uma nova instância de servidor é criada. Esta ação
demora alguns minutos para ser concluída.

**Nota**: todos os dados de sua instância de servidor anterior, incluindo informações sobre os apps e adaptadores, são persistidos na instância de serviço {{site.data.keyword.dashdbshort_notm}} configurada. Esses dados ficam disponíveis para uso depois que o servidor é recriado.

##	Definindo a configuração avançada
{: #using_mfs_advanced_p2}

Use **Iniciar servidor com a configuração avançada** na página `Visão geral` para criar o servidor com configurações avançadas ou customizadas. Também é possível
atualizar as definições do servidor para customizar a configuração do servidor clicando na
guia **Configuração**. O {{site.data.keyword.mobilefoundation_short}} fornece acesso a algumas configurações avançadas.

*	Na guia **Topologia**, é possível selecionar o tamanho de seu contêiner. O servidor padrão de 1 GB é suficiente para teste de desenvolvimento e leve.
  - Selecione o tamanho correto para seu servidor com base em sua necessidade.

  - **Nós** exibe o número de nós que são criados.
      - É possível configurar o número de nós mínimos e máximos necessários no grupo de contêiner do {{site.data.keyword.IBM_notm}}. Os grupos de contêiner fornecem alta
disponibilidade e escalabilidade.

      - O server farm do {{site.data.keyword.mobilefirst}} pode ser criado configurando o número de nós aqui.

Consulte a
documentação
do [{{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}, para obter mais detalhes.
