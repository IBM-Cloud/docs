---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Acesso ao Sistema
{: #system_access}
Estes tópicos incluem métodos de criação e gerenciamento de uma instância de serviço, junto a várias maneiras de acesso e configuração de acesso aos sistemas.
{: shortdesc}

*Última atualização: 08 de junho de 2016*
{: .last-updated}

## Uso de API REST no WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

As instâncias no WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} são criadas, provisionadas, gerenciadas e excluídas em uma das maneiras a seguir:

* A partir do Painel de catálogo e serviço do {{site.data.keyword.Bluemix_notm}} na UI do {{site.data.keyword.Bluemix_notm}}.
* A partir da criação de um aplicativo ou script que usa nossas APIs RESTful.

Por meio do uso de nossas APIs REST compatíveis com o Swagger 2.0, os clientes possuem acesso à mesma função, conforme fornecida por meio do portal e do painel. Para obter mais informações sobre APIs REST e recursos suportados, consulte a [Documentação da API REST](https://new-console.{DomainName}/apidocs/212){: new_window} do WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}.

**Nota:** depois de criar uma instância de
serviço, dependendo do tamanho de Camiseta criado, seu serviço poderá
não estar preparado imediatamente para uso. Recomenda-se consultar o campo **Status** do JSON retornado para determinar o estado atual da instância de serviço.

**Nota:** por padrão, a URL BASE da API aponta para um terminal na [Região sul dos EUA](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}. Se você estiver usando o Reino Unido ou a Região de Sydney, assegure-se de que seu aplicativo use um dos terminais a seguir:

* [Região do Reino Unido](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [Região de Sydney](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## Painel de Serviço
{: #service_dashboard}

Após criar uma instância de serviço, você será levado para o painel de serviço. Sempre é possível voltar ao painel de serviço ao clicar no ícone de serviço a partir do painel da sua organização.
A partir do painel de serviço você poe acessar:

*  Um link para esta documentação
*  Um link para fazer download dos arquivos de configuração da OpenVPN requeridos.
*  A capacidade de iniciar e parar a máquina virtual. A MV
é inicialmente iniciada.
*  O nome do host.
*  O usuário administrativo e a senha do administrador.
*  Uma chave SSH privada.
*  O usuário administrativo e a senha do administrador do WebSphere®.
*  As URLs do Admin Center e do Admin Console.

**Nota**: em razão de uma quantia específica de recursos de cálculo, de memória e de E/S, os clientes são cobrados por VMs acumuladas no estado INTERROMPIDO a uma taxa reduzida de 5%. Os clientes são gerenciados para um número fixo de instâncias INTERROMPIDAS com não mais de 10 endereços IP ou 64 GB de memória.


## Configurando a openVPN para instâncias do WebSphere Application Server for Bluemix
{: #setup_openvpn}

A OpenVPN é necessária para acessar qualquer máquina virtual do WebSphere Application Server on Bluemix. Você deve tê-la instalada e ela deve estar em execução com privilégios
de administrador.  

### Use as instruções a seguir para configurar a openVPN no Windows:

1. No link de [download da openVPN do Windows](http://swupdate.openvpn.org/community/releases/), faça download de
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} para 64 bits ou
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} para 32 bits.
2. Assegure-se de [Executar como Administrador do Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} e instale a openVPN.
3. Faça download dos arquivos de configuração da VPN a partir do link de download da OpenVPN da instância do WebSphere Application Server for Bluemix no painel de serviço. Extraia os quatro arquivos no arquivo compactado para o diretório **{OpenVPN home}\config**.   Por exemplo:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Inicie o programa cliente da openVPN "OpenVPN GUI". Assegure-se de selecionar [Executar como Administrador do Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} para iniciar o programa. Se você não o fizer, pode não ser
capaz de se conectar.

### Use as instruções a seguir para configurar a openVPN no Linux:
1. Para instalar a openVPN, siga estas [instruções](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * Se precisar fazer download e instalar manualmente o RPM Package Manager, acesse o [download do openVPN unix/linux](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. Você pode precisar de assistência de seu administrador Linux.
3. Faça download dos arquivos de configuração da VPN a partir do link de download da OpenVPN da instância do WebSphere Application Server for Bluemix no painel de serviço. Extraia os arquivos no diretório a partir do
qual você planeja iniciar o cliente OpenVPN. Você precisa de todos os quatro arquivos no mesmo
diretório.
3. Inicie o programa cliente da openVPN.  Abra uma janela do terminal e acesse o diretório que contém os arquivos de configuração. Execute o comando a seguir como root:

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Use as instruções a seguir para configurar a openVPN no Mac:
1. Um método é instalar o [Tunnelblick](https://tunnelblick.net/){: new_window}, um produto de software livre.
2. Extraia os arquivos de configuração da VPN a partir do serviço WebSphere. o Tunnelblick solicita sua senha do administrador para Mac e inclui a
configuração no conjunto de VPNs que você pode usar para se conectar.
3. Conecte-se à VPN e, em seguida, poderá acessar sua máquina virtual. Após seu primeiro acesso, o Tunnelblick armazena a configuração em cache e você pode conectar a partir do [Tunnelblick](https://tunnelblick.net/){: new_window}. É possível colocar um ícone na barra de menus para fácil acesso.


## Usando SSH para acessar as MVs do WebSphere Application Server for Bluemix
{: #using_ssh}

Estas instruções assuem que você está usando o OpenSSH como seu cliente. O OpenSSH normalmente está disponível no Linux ou no Cygwin em execução no Windows. Ele também pode ser instalado para executar a partir de um prompt de comandos do Windows.

Para verificar a instalação do OpenSSH, insira o comando:
  ```
      $ ssh -V
  ```
  {: codeblock}

Sua resposta deve ser semelhante a:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Use as instruções a seguir para configurar o acesso do SSH às VMs (máquinas virtuais) do WebSphere Application Server for Bluemix

1. Revise a mensagem de aviso que aparece na primeira vez em que você conecta, "A autenticidade do host x.x.x.x não pode ser estabelecida." Isto é
normal. Quando solicitado, selecione sim. A chave pública está agora instalada em sua VM (máquina virtual) para o usuário virtuser.
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

Ao clicar no link para o Admin Center ou o Admin Console, você pode receber um aviso de *Conexão não confiável*. A mensagem exata varia de acordo
com o navegador, assim como as etapas exatas para efetuar bypass ou eliminar o aviso.

Como você está usando links fornecidos pela {{site.data.keyword.IBM}}, poderá ignorar o aviso com segurança e conectar. Se o seu navegador oferecer armazenar
a exceção de segurança, fazê-lo é a maneira mais fácil de evitar o aviso no futuro.

Outra opção é exportar o certificado de assinante recebido e, então, importá-loem seu navegador como um certificado raiz confiável. Essa opção requer que você crie uma entrada em seu arquivo *hosts* que mapeie o endereço IP da VM (máquina virtual) para o nome comum do emissor do certificado. Esse nome está no formato a seguir: wl<pureapplication.ibmcloud.com. Se você agora usar o nome do host em vez do endereço IP na URL,
você deve se conectar sem problemas. Você, então, tem acesso ao Centro Administrativo ou
ao Console Administrativo usando o nome do host em vez do endereço IP na URL.

Finalmente, os clientes frequentemente instalam seus próprios certificados raiz para
aplicativos que eles tornam externos. Para obter mais informações, consulte o [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} ou o [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center.

## Portas Firewall
{: #firewall_ports}

Talvez seja necessário abrir portas no firewall para permitir acesso a aplicativos e
bancos de dados.
  * Em cada nó do WebSphere Application Server for Bluemix, você localiza um script openFirewallPorts.sh no diretório WAS_HOME/virtual/bin.
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

**Nota**: tanto sport como dport da porta aberta são abertos nas seções INPUT e OUTPUT do firewall. Deve-se executar esse script como raiz usando sudo. Também é possível
modificar iptables diretamente.
