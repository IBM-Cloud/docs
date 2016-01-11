# Criando apps móveis
{: #mobile}

Com o {{site.data.keyword.Bluemix_notm}} Mobile Services, é possível incorporar serviços de nuvem pré-construídos, gerenciados e escaláveis nos aplicativos móveis sem depender do envolvimento de TI. Você pode focar na
construção dos seus apps móveis em vez de nas complexidades de gerenciamento da
infraestrutura de backend.

<table><caption>Tabela 1. texto padrão do Bluemix Mobile Services</caption>
<tr>
	<td>Cada um dos Bluemix Mobile Services pode ser usado independentemente. Também é possível usá-los em conjunto para obter o maior benefício. Para iniciar, use o Texto padrão do Bluemix Mobile Services para criar seu app. Este texto padrão:
		<ul>
			<li>Cria um tempo de execução Node.js com um aplicativo modelo. É possível usar esse aplicativo para fornecer funções do lado do servidor, como APIs RESTful e arquivos estáticos. É possível ler mais sobre como operar esse aplicativo na seção Desenvolvendo backend móvel. </li>
			<li>
Provisiona uma instância de cada um dos Bluemix Mobile Services e liga o serviço ao aplicativo Node.js. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> Texto padrão do Bluemix Mobile Services </td>
</tr>
</table>

Depois de usar o Texto padrão do Bluemix Mobile Services para criar seu app, é possível obter amostras de HelloWorld para cada um dos serviços ou iniciar a instrumentação de seu app existente para usar os serviços Bluemix.


## Visão Geral de Serviços
{: #services-overview}
É possível usar todos os Bluemix Mobile Services juntos usando o Texto padrão do Bluemix Mobile Services ou usar serviços individuais do catálogo do Bluemix. O diagrama a seguir descreve todos os componentes do Bluemix Mobile Services.

![Arquitetura do Bluemix mobile services](images/bms_architecture.jpg)

<table>
<caption>Tabela 2. Bluemix e sistemas corporativos</caption>
<th>Bluemix</th>
<th>Sistemas corporativos</th>
<tr>
<td> <img src="images/i_js_64.png" alt="ícone de tempo de execução Node.js"><b>Node.js</b> <br/> Um tempo de execução Node.js que hospeda um app modelo é fornecido como parte do texto padrão do Bluemix Mobile Services. É possível usar o aplicativo modelo para fornecer funções do lado do servidor, como APIs RESTful e arquivos estáticos. <br/>Por exemplo, é possível ampliar o aplicativo Node.js para processamento de lógica customizada ou para se conectar às APIs REST na infraestrutura existente de sua empresa. Cada app criado no Bluemix tem um ID de app exclusivo. Seu app móvel usa esse ID com o SDK para acessar os serviços associados a esse aplicativo. O ID do app é usado pela plataforma como o contexto para funções comuns, como medição e criação de log.
É possível ler mais sobre como operar esse aplicativo na seção "Desenvolvendo backend móvel".</td>
<td valign="top"><b>Provedores de informações</b> <br/>É possível usar um tempo de execução Node.js que se hospedou no Bluemix para se conectar a qualquer tipo de provedor de informações:
<ul>
	<li>Backend corporativo</li>
	<li>Base de dados </li>
	<li>Outro serviço de terceiro hospedado</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="ícone de serviço do Mobile Client Access"> <b>Mobile Client Access</b><br/>Use o serviço IBM Mobile Client Access for Bluemix para proteger os aplicativos Node.js e Java for Liberty hospedados no Bluemix. Ao instrumentar seu app móvel com o SDK do Mobile Client Access, é possível requerer que os usuários efetuem login para acessar o Node.js ou o Bluemix Mobile Services. Além dos recursos de segurança, o Mobile Client Access também reúne dados de analítica, para que seja possível monitorar o desempenho do aplicativo móvel e coletar logs do cliente e estatísticas de uso. </td>
<td valign="top"><b>Provedores de identidade do usuário</b> <br/>É possível usar os provedores de identidade a seguir: <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="ícone de serviço de Push Notifications"> <b>Push Notifications</b><br/>O serviço IBM Push Notifications for Bluemix fornece uma plataforma unificada para enviar e gerenciar notificações push móveis que são destinadas às plataformas iOS e Android. Esse serviço gerencia o mapeamento dos usuários do aplicativo para seus dispositivos, plataforma de dispositivo e manipula o despacho de notificações push para os dispositivos. Com esse serviço, é possível enviar transmissões, unicasts (com base no userID, deviceID) e tags (ou tópicos) com base em notificações push para os usuários do aplicativo móvel.</td>
<td valign="top"><b>Provedores de serviços de push</b><ul><li>Serviço Apple Push Notifications</li><li>Sistema de mensagens em nuvem do Google</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="ícone de serviço do Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant é um NoSQL database as a service (DBaaS). Ele é construído
a partir do zero para escalar globalmente, executar sem interrupção e manipular uma grande variedade de tipos
de dados como JSON, texto completo e geoespacial. </td>
<td>Cloudant.com</td>
</tr>
</table>
