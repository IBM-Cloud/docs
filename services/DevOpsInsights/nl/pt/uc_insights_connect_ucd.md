---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conectando servidores IBM UrbanCode Deploy ao Delivery Insights
{: #connect_ucd}

Para ver dados de um servidor IBM UrbanCode Deploy no Delivery Insights, deve-se instalar uma correção no servidor e, em seguida, conectar esse servidor ao DevOps Connect.
{:shortdesc}

## Antes de iniciar

- Veja os [pré-requisitos](uc_insights_prereqs.html), incluindo a configuração de uma instância do DevOps Connect.
- Seu servidor IBM UrbanCode Deploy deve estar na versão 6.2 ou mais recente.

## Procedimento

1. Instale a correção no servidor IBM UrbanCode Deploy. Todas as versões do IBM UrbanCode Deploy requerem uma correção para se comunicar com o DevOps Connect. 
  1. Faça download da correção correta para sua versão do IBM UrbanCode Deploy acessando a página a seguir e fazendo download da correção correta:
  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Extraia o arquivo. Ele contém um ou mais arquivos de correção que devem ser incluídos no servidor.

  1. Pare o servidor. Veja [Iniciando e parando o servidor](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Coloque os arquivos de correção na pasta <code><em>application_data</em>/patches</code>, em que <code><em>application_data</em></code> é a pasta de dados do aplicativo do servidor. A pasta de dados do aplicativo padrão é `/opt/ibm-ucd/server/appdata` no Linux e `C:\Program Files\ibm-ucd\server\appdata` no Windows. Em sistemas de alta disponibilidade, a pasta de dados do aplicativo está sempre em uma unidade de rede compartilhada que cada servidor pode acessar.

  1. Opcional: enquanto o servidor estiver interrompido, para aumentar o desempenho da importação de dados desse servidor, execute os comandos SQL a seguir no banco de dados:  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  Use o nome de seu banco de dados para `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Inicie o servidor. 

    **Nota:** talvez seja necessário esperar mais do que o normal para o servidor IBM UrbanCode Deploy iniciar. Se o servidor não for finalmente iniciado ou não estiver funcionando corretamente, exclua os arquivos de correção e reinicie o servidor. Os arquivos de correção não afetam permanentemente o servidor.

1. Algumas versões do IBM UrbanCode Deploy requerem uma correção adicional para que o servidor se conecte ao DevOps Connect. Se estiver usando o IBM UrbanCode Deploy versão 6.2 à 6.2.1.2, a correção adicional a seguir deverá ser instalada no servidor:
  1. Faça download da correção: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Pare o servidor.
  1. Coloque o arquivo de correção na pasta <code><em>application_data</em>/patches</code>.
  1. Inicie o servidor.

1. Crie uma integração entre o DevOps Connect e o servidor IBM UrbanCode Deploy:  
  **Importante:** na primeira vez que a integração for executada, o DevOps Connect recuperará dados dos 90 dias anteriores. Se você tiver uma grande quantia de dados de implementação, esse processo poderá levar muito tempo. Para recuperar dados para menos de 90 dias, veja [Resolução de problemas](uc_insights_connect_ucd.html#troubleshooting).
  1. No IBM UrbanCode Deploy, crie um token de autenticação. Veja [Tokens](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. No DevOps Connect, clique em **Integrações** e, em seguida, clique em **Incluir novo**.
  1. Especifique um nome e uma descrição para a integração. O local padrão do DevOps Connect é `https://hostname:8443/`, em que `hostname` é o nome do host do sistema que hospeda o DevOps Connect.
  1. Na lista **Tipo de integração**, selecione **IBM UrbanCode Deploy for Cloud Reporting**.
  1. No campo **URI do servidor**, insira a URL pública do servidor IBM UrbanCode Deploy, como `https://my_UCD.example.com:8447`.
  1. No campo **Token de autenticação**, insira ou cole o token de autenticação que foi gerado pelo IBM UrbanCode Deploy.
  1. No campo **Usuário administrador**, insira uma lista separada por vírgula de IBMids para fornecer acesso à interface do DevOps Connect.
  1. Opcional: clique em **Executar integração** para executar a integração imediatamente. Por padrão, as integrações são executadas a cada minuto.
  1. Clique em **Salvar**.

  ![Configurando a integração no DevOps Connect](images/uc_insights_dc_integration.gif)

Agora seus dados estão sincronizados com o Delivery Insights. Agora é possível criar e visualizar relatórios que se baseiam nesses dados.

## Resolver problemas
{: #troubleshooting}

Se várias solicitações de aplicativos e de processos do componente forem armazenadas no banco de dados do servidor IBM UrbanCode Deploy, poderão ocorrer erros durante o processo de recuperação. Uma mensagem semelhante ao texto a seguir é gravada no log de saída do servidor:

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Para contornar esse comportamento, edite o arquivo `plugin.properties` para que o plug-in reduza o número de dias de dados válidos a serem recuperados. O arquivo `plugin.properties` está no diretório `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` no computador em que o DevOps Connect foi instalado. Edite a linha a seguir para remover o sinal de número (#) e reduzir o número de dias:

`#numDaysToRetrieve=90`

Por exemplo, mude a linha para o texto a seguir para recuperar apenas os 30 dias anteriores de dados válidos:

`numDaysToRetrieve=30`

Salve o arquivo e, em seguida, execute a integração novamente. Verifique os logs do servidor para assegurar-se de que o erro não ocorra mais.
