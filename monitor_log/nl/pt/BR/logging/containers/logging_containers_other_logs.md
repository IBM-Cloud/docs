---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Coletando dados do log não padrão de um contêiner
{: #logging_containers_collect_data}

Para capturar dados de locais de log não padrão dentro de um contêiner, configure a variável de ambiente **LOG_LOCATIONS** ao criar um contêiner. 
{:shortdesc}

* Inclua a variável de ambiente **LOG_LOCATIONS** com um caminho para o arquivo de log quando criar o contêiner. 
* É possível incluir múltiplos arquivos de log separando-os com vírgulas. 

## Coletando dados do log não padrão por meio do console do Bluemix
{: #logging_containers_collect_data_ui}

Conclua as etapas a seguir para coletar dados não padrão por meio do console:

1. No catálogo, selecione **Contêineres** e escolha uma imagem. 

    A lista de imagens que são exibidas inclui imagens que são fornecidas pela {{site.data.keyword.IBM}} e imagens que estão armazenadas em seu registro privado do {{site.data.keyword.Bluemix_notm}}. 

2. Defina seu contêiner. Escolha o tipo, insira um nome para o contêiner, selecione seu tamanho e defina outros atributos, como detalhes e portas de endereço IP. Para obter mais informações, veja [Criar e implementar um contêiner único por meio da UI do {{site.data.keyword.Bluemix_notm}}](/docs/containers/container_single_ui.html#gui). 

3. Expanda a seção **Opções avançadas** e selecione **Incluir uma nova variável de ambiente**.

4. Inclua a variável **LOG_LOCATIONS** e configure seu valor para o log que deseja analisar.

    Por exemplo, ao incluir um contêiner que se baseia na imagem mais recente do Liberty, para analisar o arquivo de log *dpkg.log*, configure o valor de ambiente para o seguinte:
    
    <table>
      <caption>Tabela 1. Valor de amostra de locais de log</caption>
      <tbody>
        <tr>
          <th align="center">Nome da variável</th>
          <th align="center">Valor</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. Clique **Criar**.

O painel do contêiner é aberto. Verifique se o status do contêiner é *Executando* e, em seguida, verifique os logs na guia **Monitoramento e logs**.


## Coletando dados do log não padrão por meio da CLI
{: #logging_containers_collect_data_cli}

Conclua as etapas a seguir para coletar dados do log não padrão por meio da CLI:

1. Configure um terminal para usar a CLI do {{site.data.keyword.containershort}}. Para obter mais informações, consulte [Configurando a CLI do IBM Bluemix Container Service](/docs/containers/container_cli_cfic_install.html).

2. Efetue login na CLI do Cloud Foundry usando o comando a seguir: `cf login`. Insira seu ID, sua senha, sua organização e seu espaço do {{site.data.keyword.Bluemix_notm}} quando forem solicitados. 

    Por padrão, você é conectado à região sul dos EUA ou à última região na qual efetuou login. 
    
    É possível incluir a opção **-a** para efetuar login em uma região específica no {{site.data.keyword.Bluemix_notm}}. Por exemplo, a tabela a seguir lista os comandos por região:

    <table>
      <caption>Tabela 2. Comandos por região</caption>
      <tbody>
        <tr>
          <th align="center">Região</th>
          <th align="center">Comando:</th>
        </tr>
        <tr>
          <td align="left">Sul dos EUA</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">Reino Unido</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
	 <tr>
          <td align="left">Frankfurt</td>
          <td align="left">cf login -a api.eu-de.bluemix.net</td>
        </tr>
       </tbody>
    </table>
    

3. Efetue login no {{site.data.keyword.containershort}} usando o comando a seguir: `cf ic login`

4. Crie um contêiner único por meio de uma imagem. Inclua a variável de ambiente LOG_LOCATIONS para incluir locais de log não padrão.  

    Para incluir um local customizado para que seja possível visualizar essas informações de log no Kibana, inclua a variável de ambiente **LOG_LOCATIONS** ao criar o contêiner. Insira o comando a seguir:
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    em que
    
     <table>
      <caption>Tabela 3. Opções de comando</caption>
      <tbody>
        <tr>
          <th align="center">Opção</th>
          <th align="center">Descrição</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> Se desejar tornar seu app acessível na Internet, será necessário expor uma porta pública. Inclua quaisquer portas que sejam especificadas no Dockerfile para a imagem que está sendo usada. <br> É possível escolher entre UDP e TCP para indicar o protocolo IP que você deseja usar. Se você não especificar um protocolo, a porta será automaticamente exposta para tráfego TCP. <br> Ao expor uma porta pública, você cria um Grupo de segurança de rede pública para seu contêiner que permite enviar e receber dados públicos somente na porta exposta. Todas as outras portas públicas estão encerradas e não podem ser usadas para acessar seu app na Internet. <br> É possível incluir múltiplas portas com múltiplas opções -p. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">Configurar uma variável de ambiente. <br> É possível listar múltiplas chaves separadamente. Inclua aspas em torno do nome da variável de ambiente e do valor. <br> Para incluir um arquivo de log para que seja monitorado no contêiner, inclua a variável de ambiente LOG_LOCATIONS com um caminho no arquivo de log.</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">Define o nome do contêiner.</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">Registro na região pública. Por exemplo, para a região sul dos EUA, o nome de domínio padrão é: `ng.bluemix.net` e, para o Reino Unido, o nome de domínio padrão é: `eu-gb.bluemix.net` </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">Nome da imagem que deseja incluir.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">Tag da imagem que deseja incluir.</td>
        </tr>
      </tbody>
    </table>
    
    Por exemplo, para criar um contêiner com base na imagem mais recente do Liberty e incluir o arquivo de log `/var/log/dpkg.log`, use o comando a seguir: 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    O arquivo dpkg.log é um arquivo de log padrão do Ubuntu que normalmente é gerado durante a criação de um contêiner, mas não é enviado por push automaticamente para o Kibana.

Para verificar o status do contêiner, execute o comando `docker ps`. Quando o status for *Executando*, verifique os logs no console do {{site.data.keyword.Bluemix_notm}} por meio da linha de comandos ou por meio do Kibana.



