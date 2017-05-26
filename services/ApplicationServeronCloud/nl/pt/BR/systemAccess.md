---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Acesso ao Sistema
{: #system_access}


Métodos de criar e gerenciar uma instância de serviço são discutidos nessa seção, juntamente com várias formas de acessar e configurar o acesso aos seus sistemas.
{: shortdesc}


## Uso de API de REST no WebSphere Application Server no {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

As instâncias no WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} são criadas, provisionadas, gerenciadas e excluídas de uma das formas a seguir:

* A partir do Painel de catálogo e serviço do {{site.data.keyword.Bluemix_notm}} na UI do {{site.data.keyword.Bluemix_notm}}.
* Por meio da criação de um aplicativo ou script que usa APIs RESTful.


Por meio do uso de APIs REST compatíveis com o Swagger 2.0, os clientes têm acesso à mesma função conforme fornecido no portal e no painel. Para obter mais informações sobre APIs de REST e recursos suportados, consulte a {{site.data.keyword.Bluemix_notm}}[Documentação de API de REST do WebSphere Application Server](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}. Para o código de amostra que demonstra o uso das APIs de REST, faça download das {{site.data.keyword.Bluemix_notm}} [Amostras de API de REST](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window} do WebSphere Application Server hospedado no Git.

**Nota:** depois de criar uma instância de
serviço, dependendo do tamanho de Camiseta criado, seu serviço poderá não estar imediatamente pronto para uso. Recomenda-se consultar o campo **Status** do JSON retornado para determinar o estado atual da instância de serviço.

**Nota:** a URL **apiEndpoint** referenciada em [Amostras de API REST](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window} aponta para a região sul
dos EUA. Se estiver usando outras regiões, assegure-se de que seu aplicativo referencie a URL **apiEndpoint** apropriada.

*Tabela 1. URLs de terminal de API para implementação de API Rest*

| **Nome da região** | **Local geográfico** | **Prefixo da região** | **URL de terminal de API** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| SUL dos EUA | Dallas, TX, EUA | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| Reino Unido | Londres, Inglaterra | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| Sydney | Sydney, Austrália | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| Frankfurt | Frankfurt, Alemanha | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## Painel de Serviço
{: #service_dashboard}

Após criar uma instância de serviço, você será levado para o painel de serviço. Sempre é possível voltar ao painel de serviço ao clicar no ícone de serviço a partir do painel da sua organização.
A partir do painel de serviço você poe acessar:

* Um link para esta documentação
* Um link para fazer o download dos arquivos de configuração OpenVPN necessários
* A capacidade de iniciar e parar a máquina virtual. A VM é ativada inicialmente.
* O nome do host
* O usuário administrativo e a senha administrativa
* Uma chave SSH privada
* O usuário administrativo e a senha administrativa do WebSphere®
* As URLs do Admin Center e do Admin Console

**Nota**: devido a uma quantia específica de recursos de cálculo, memória e E/S, os clientes são cobrados por VMs acumuladas no estado INTERROMPIDO a uma taxa reduzida de
5%. Os clientes são gerenciados a um número fixo de instâncias de INTERROMPIDO com até 10 endereços IP ou 64 GB de memória.


## Configurando a openVPN para instâncias do WebSphere Application Server no Bluemix
{: #setup_openvpn}

A OpenVPN é necessária para acesso a qualquer máquina virtual do WebSphere Application Server no Bluemix. Ela deve estar instalada e em execução com privilégios de administrador.

### Use as instruções a seguir para configurar a openVPN no Windows:

1. No link de [download da openVPN do Windows](http://swupdate.openvpn.org/community/releases/), faça download de
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} para 64 bits ou
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} para 32 bits.
2. Assegure-se de [Executar como um administrador do Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} e que a openVPN esteja
instalada.
3. Faça download dos arquivos de configuração de VPN por meio do link de download da OpenVPN da instância do WebSphere Application Server no Bluemix no painel de serviço. Extraia os quatro arquivos no arquivo compactado para o diretório **{OpenVPN home}\config**. Por exemplo:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Inicie o programa cliente da openVPN "OpenVPN GUI". Assegure-se de selecionar [Executar como Administrador do Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} para iniciar o programa. Se você não o fizer, pode não ser
capaz de se conectar.

### Use as instruções a seguir para configurar a openVPN no Linux:
1. Para instalar a openVPN, siga as [instruções](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * Se precisar fazer download e instalar manualmente o RPM Package Manager, acesse o [download do openVPN unix/linux](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. Você pode precisar de assistência de seu administrador Linux.
3. Faça download dos arquivos de configuração de VPN por meio do link de download da OpenVPN da instância do WebSphere Application Server no Bluemix no painel de serviço. Extraia os arquivos no diretório a partir do
qual você planeja iniciar o cliente OpenVPN. Você precisa de todos os quatro arquivos no mesmo
diretório.
3. Inicie o programa cliente da openVPN. Abra uma janela do terminal e acesse o diretório que contém os arquivos de configuração. Execute o comando a seguir como root:

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Use as instruções a seguir para configurar a openVPN no Mac:
1. Um método é instalar o [Tunnelblick](https://tunnelblick.net/){: new_window}, um produto de software livre.
2. Extraia os arquivos de configuração da VPN a partir do serviço WebSphere. o Tunnelblick solicita sua senha do administrador para Mac e inclui a
configuração no conjunto de VPNs que você pode usar para se conectar.
3. Conecte-se à VPN e, em seguida, poderá acessar sua máquina virtual. Após seu primeiro acesso, o Tunnelblick armazena a configuração em cache e você pode conectar a partir do [Tunnelblick](https://tunnelblick.net/){: new_window}. É possível colocar um ícone na barra de menus para fácil acesso.


## Usando SSH para acessar VMs do WebSphere Application Server no Bluemix
{: #using_ssh}

Estas instruções assuem que você está usando o OpenSSH como seu cliente. O OpenSSH normalmente está disponível no Linux ou no Cygwin em execução no Windows. Ele também pode ser instalado para executar a partir de um prompt de comandos do Windows.

Para verificar a instalação do OpenSSH, insira o comando:
  ```
      $ ssh -V
  ```
  {: codeblock}

A mensagem a seguir é um exemplo da resposta:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Use as instruções a seguir para configurar o acesso SSH a suas VMs do WebSphere Application Server no Bluemix

1. Revise a mensagem de aviso que aparece na primeira vez em que você conecta, "A autenticidade do host x.x.x.x não pode ser estabelecida." Essa mensagem é normal. Quando solicitado, selecione sim. A chave pública está agora instalada em sua VM (máquina virtual) para o usuário virtuser.
2. Efetue login no virtuser usando a chave privada. Para melhores resultados, use o método de autenticação de chave privada.
3. Copie o conteúdo da chave privada em um arquivo.
4. Execute o
comando:

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName
  </pre>
  {: codeblock}

5. Obtenha autoridade integral de sysadmin alternando virtuser para root usando o comando:

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. Se você tiver problemas ao acessar o sistema com a chave ssh privada, use a senha raiz que é fornecida. Efetue login como root executando o comando a seguir e forneça a senha.

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. Quer você acesse o sistema com a chave ssh privada
ou com a senha raiz, mude imediatamente a senha raiz.
8. Para simplificar seus comandos SSH, crie um arquivo chamado "config" no diretório %HOME%/.ssh. Por exemplo:

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /path/privateKeyFileName
  </pre>
  {: codeblock}

9. Execute "ssh VM1" para ser conectado como virtuser.

## Caminhos do Sistema
{: #system_paths}

* Os comandos do Liberty Profile podem ser emitidos a partir do */opt/IBM/WebSphere/Liberty/bin*.
* O local do perfil do servidor Liberty Profile é */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*.
* Os comandos do Traditional WebSphere Application Server podem ser emitidos a partir de */opt/IBM/WebSphere/AppServer/bin*.
* O local do perfil do Traditional WebSphere Application Server do servidor é */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Usando os link do Centro Administrativo e do Console Administrativo
{: #console_links}

Ao clicar no link para o Admin Center ou Admin Console, será possível que receba um aviso de *Conexão não confiável*. A mensagem exata varia de acordo
com o navegador, assim como as etapas exatas para efetuar bypass ou eliminar o aviso.

Uma vez que você está usando links que são fornecidos pelo {{site.data.keyword.IBM}}, é possível ignorar o aviso e se conectar com segurança. Se o seu navegador oferecer armazenar
a exceção de segurança, fazê-lo é a maneira mais fácil de evitar o aviso no futuro.

Outra opção é exportar o certificado de assinante recebido e, então, importá-loem seu navegador como um certificado raiz confiável. Essa opção requer que você crie uma entrada em seu arquivo *hosts* que mapeie o endereço IP da VM (máquina virtual) para o nome comum do emissor do certificado. Esse nome está no formato a seguir: wl<pureapplication.ibmcloud.com. Se agora o nome do host for usado em vez do endereço IP na URL, será possível se conectar sem problemas. O Admin Center ou o Admin Console devem ser acessados usando esse nome do host em vez do endereço IP na URL.

Finalmente, os clientes frequentemente instalam seus próprios certificados raiz para
aplicativos que eles tornam externos. Para obter mais informações, consulte o IBM Knowledge Center do [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} ou do [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window}.

## Portas Firewall
{: #firewall_ports}

Talvez seja necessário abrir portas no firewall para permitir acesso a aplicativos e
bancos de dados.
  * Em cada nó do WebSphere Application Server no Bluemix, você localiza um script openFirewallPorts.sh no diretório WAS_HOME/virtual/bin.
  * Em cada host do Liberty Collective, você localiza um script openFirewallPorts.sh no diretório WAS_HOME/virtual/bin.

Uso:
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT é o número da porta
* PROTOCOL é TCP ou UDP
* -persist é true ou false

Para especificar várias portas, separe-as
com uma vírgula ","

**Nota**: a porta s e porta d da porta que está aberta são abertas nas seções de ENTRADA e SAÍDA do firewall. Deve-se executar esse script como raiz usando sudo. Também é possível
modificar iptables diretamente.

## Configurando o servidor da web
{: #configure_webserver}

Ao provisionar uma célula ou um coletivo, você receberá um ambiente pré-configurado. Especificamente, para uma célula do Network Deployment tradicional, você recebe o ambiente a seguir:

* Um Gerenciador de Implementação que está colocado com o IBM HTTP Server para propósitos de desenvolvimento e de teste.

* Um nó customizado federado ao Gerenciador de Implementação.

* O Gerenciador de Implementação, o Servidor IHS e o Agente do Nó são todos inicialmente provisionados ao estado INICIADO.

Se o servidor da web for necessário para manipular todas as solicitações do usuário, então poderá ser necessário gerar e propagar o plug-in após a implementação do seu aplicativo.

**Evite problemas:** antes de gerar e propagar o plug-in, assegure-se de que as tarefas de pré-requisito a seguir estejam concluídas:

* Em seu ambiente Windows, Linux ou MAC local, assegure-se de que a [openVPN](systemAccess.html#setup_openvpn) esteja configurada, iniciada e que você esteja conectado à região adequada.

* No Painel de serviço do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}}, clique em **Abrir o console administrativo** e efetue login com wsadmin e a Senha de administrador fornecida no Painel de serviço.

* Por meio do Admin Console, crie um servidor de aplicativos (por exemplo, ***server1***), porque o Gerenciador de Implementação é federado com um nó customizado vazio.

* Inicie o servidor que você criou.

* Durante a instalação do aplicativo, assegure-se de que os módulos de seu aplicativo estejam mapeados para o servidor que você acabou de iniciar e para o servidor da web (por exemplo,
***webserver1***).

As etapas a seguir de alto nível presumem que as tarefas de pré-requisito estejam concluídas:

1. Por meio do Admin Console, gere o plug-in a partir da opção Ambiente:
   1. Escolha Ambiente > Atualizar configuração global do plug-in de servidor da web
   2. Clique em **OK** ou **Sobrescrever para gerar um novo arquivo de configuração de plug-in**
2. Por meio do Gerenciador de Implementação, copie o plug-in na configuração do servidor da web:

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. Edite **httpd.conf** em **IHS_HOME/conf** (por exemplo, */opt/IBM/WebSphere/HTTPServer/conf*) e assegure-se de que as duas linhas a
seguir existam:

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. Abra as portas com esses dois comandos:

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. Pare e inicie o servidor da web com os dois comandos a seguir:
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. Acesse seu aplicativo por meio do plug-in:
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**NOTA:** as etapas que são fornecidas representam um caminho de muitos na tentativa de configurar um servidor da web. Se for necessária assistência adicional, consulte o [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window}.

**NOTA:** se não é possível acessar seu aplicativo, provavelmente você está tendo um problema de acesso de porta em seu firewall. Portanto, pode ser necessário reiniciar qualquer um dos servidores a seguir: o servidor de aplicativos, o agente do nó, o servidor da web e o gerenciador de implementação. Além
disso, é possível que precise acessar o Painel de serviço do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} e reinicie cada máquina virtual.

## Configuração do SSL
{: #ssl_configuration}

O Traditional WebSphere Application Server e o perfil Liberty são configurados com o protocolo [SSL_TLSv2](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/protocols.html){: new_window}. Para mudar o protocolo, modifique as regras a seguir:

Para o Traditional WebSphere Application Server:

1. Edite **security.xml** em /opt/IBM/WebSphere/Profiles/*profile_name*/config/cell/*cell_name* e modifique a linha a seguir:

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}

2. Edite **ssl.client.props** em /opt/IBM/WebSphere/Profiles/*profile_name*/properties e modifique a linha a seguir:

  ```
  com.ibm.ssl.protocol=SSL_TLSv2
  ```
{: codeblock}

Para o perfil Liberty:

1. Edite **server.xml** em /opt/IBM/WebSphere/Profiles/Liberty/servers/server1 e modifique a linha a seguir localizada no elemento de configuração defaultSSLConfig ssl:

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}
