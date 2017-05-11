---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Exemplo: transmitindo logs do aplicativo Cloud Foundry para o Splunk
{: #splunk}

Neste exemplo, uma desenvolvedora chamada Jane cria um servidor virtual usando o IBM Virtual Servers Beta e a imagem do Ubuntu.  A Jane tenta transmitir logs do aplicativo Cloud Foundry a partir do
{{site.data.keyword.Bluemix_notm}} para o Splunk.
{:shortdesc}

  1. Para começar, a Jane configura o Splunk.

     a. A Jane faz download do Splunk Light por meio do [Site de Download do Splunk Light ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} e, em seguida, o instala usando o comando a seguir. O software é instalado em */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. A Jane instala e corrige o complemento de tecnologia de syslog RFC5424 para integrar com o {{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre as instruções para instalar o complemento, veja a [Diretriz do Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    A Jane instala o complemento usando os comandos a seguir:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Em seguida, a Jane corrige o complemento substituindo */opt/splunk/etc/apps/rfc5424/default/transforms.conf* por um novo arquivo *transforms.conf* que consiste no
texto a seguir:

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Após o Splunk ser configurado, a Jane deve abrir algumas portas na máquina do Ubuntu para aceitar o dreno de syslog recebido (porta 5140) e a UI da World Wide Web do Splunk (porta 8000) porque
o servidor virtual {{site.data.keyword.Bluemix_notm}} possui o firewall configurado por padrão.

	    **Nota:** A configuração de iptable é feita aqui para propósitos de avaliação da Jane e é provisória. Para definir a configuração de firewall no servidor virtual Bluemix em produção, veja a documentação [Network Security Groups ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} para obter detalhes.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Em seguida, a Jane executa o Splunk usando o comando a seguir:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. A Jane define as configurações do Splunk para aceitar o dreno de syslog a partir do {{site.data.keyword.Bluemix_notm}}. Ela deve criar uma entrada de dados para o dreno de syslog.

     a. A partir da interface da web do Splunk, a Jane clica em **Dados > Entradas de dados**. Uma lista de tipos de entrada que o Splunk suporta é exibida.

     b. Ela seleciona **TCP**, porque o dreno de syslog usa o protocolo TCP.

     c. Na área de janela **TCP**, ela insere **5140** no campo **Porta**, deixa os campos restantes em branco e, em seguida, clica em
**Avançar**.

     d. A partir da lista de **Tipos de Origem**, ela seleciona **Não categorizados > rfc5424_syslog**.

     e. Para o tipo de **Método**, ela seleciona **IP**.

     f. No campo de **Índice**, a Jane clica em **Criar um novo índice**. Ela nomeia o novo índice "bluemix" e, em seguida, clica em
**Salvar**.

     g. Finalmente, na janela **Revisar**, a Jane confirma que a configuração está correta e, em seguida, clica em **Enviar** para ativar essa entrada de dados.

  3. Em {{site.data.keyword.Bluemix_notm}}, a Jane cria um serviço de dreno de syslog e liga o serviço a um aplicativo.

     a. A Jane cria um serviço de dreno de syslog usando o comando a seguir a partir da interface da linha de comandos de cf:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Nota:** *dummyhost* não é o nome real. Ele é usado para ocultar o nome do host real.

     b. A Jane liga o serviço de dreno de syslog a um aplicativo em seu espaço e, em seguida, organiza novamente o aplicativo.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


A Jane testa o seu aplicativo e, em seguida, digita a sequência de consultas a seguir na interface da web do Splunk:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

A Jane vê um fluxo de logs em sua interface da web do Splunk. Embora o Splunk que a Jane instala seja o Splunk Light, ela ainda pode reter 500 MB de logs por dia.

