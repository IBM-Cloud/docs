# Criando aplicativos móveis a partir do modelo {{site.data.keyword.mobilefirstbp}} Starter
{: #try_mobile}
Última atualização: 18 de julho de 2016
{: .last-updated} 

É possível usar cada um dos Serviços móveis do {{site.data.keyword.Bluemix}} de forma independente. Também é possível usá-los
juntos, com o modelo do {{site.data.keyword.mobilefirstbp}} Starter, para se beneficiar ao máximo. 

Para começar, use o {{site.data.keyword.mobilefirstbp}} Starter para criar seu aplicativo. O modelo permite concluir as ações a
seguir:

* Crie um tempo de execução Node.js com um aplicativo modelo. É possível usar esse aplicativo para fornecer funções do lado do servidor, como APIs RESTful e arquivos estáticos. <!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* Provisione uma instância de cada um dos Serviços móveis do {{site.data.keyword.Bluemix_notm}} e ligue o serviço ao aplicativo Node.js.

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate 
-->

Após usar o modelo do {{site.data.keyword.mobilefirstbp}} Starter para criar seu aplicativo, é possível obter amostras Hello Bluemix para cada um dos serviços ou iniciar a instrumentação do seu aplicativo existente para usar serviços {{site.data.keyword.Bluemix_notm}}.


## Visão Geral de Serviços
{: #services-overview}
É possível usar todos os Serviços móveis do {{site.data.keyword.Bluemix_notm}} juntos usando o modelo do {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter ou é possível usar serviços individuais a partir do catálogo {{site.data.keyword.Bluemix_notm}}. O
diagrama a seguir descreve os componentes dos Serviços móveis do {{site.data.keyword.Bluemix_notm}}.

![Arquitetura dos serviços móveis do {{site.data.keyword.Bluemix_notm}}](images/bms_architecture.jpg)

<table summary="Esta tabela descreve os Serviços móveis do {{site.data.keyword.Bluemix_notm}}">
<caption>Tabela 1. {{site.data.keyword.Bluemix_notm}} e sistemas corporativos</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>Sistemas corporativos</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js runtime icon"><b>Node.js</b> <br/> Um tempo de execução do Node.js que hospeda um aplicativo de modelo é fornecido como parte do modelo do {{site.data.keyword.mobilefirstbp}} Starter. É possível usar o aplicativo modelo para fornecer funções do lado do servidor, como APIs RESTful e arquivos estáticos. <br/>Por exemplo, é possível ampliar o aplicativo Node.js para processamento de lógica customizada ou para se conectar às APIs REST na infraestrutura existente de sua empresa. Cada aplicativo criado no {{site.data.keyword.Bluemix_notm}} tem um ID de aplicativo exclusivo. Seu app móvel usa esse ID com o SDK para acessar os serviços associados a esse aplicativo. O ID do app é usado pela plataforma como o contexto para funções comuns, como medição e criação de log.
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>Provedores de informações</b> <br/>É possível usar um tempo de execução do Node.js hospedado em{{site.data.keyword.Bluemix_notm}} para conectar-se a qualquer tipo de provedor de informações:
<ul>
	<li>Backend corporativo</li>
	<li>Base de dados </li>
	<li>Outro serviço de terceiro hospedado</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} ícone de serviço"> <b>{{site.data.keyword.amashort}}</b><br/>Use o serviço {{site.data.keyword.amafull}} para proteger aplicativos Node.js e Java for Liberty hospedados no {{site.data.keyword.Bluemix_notm}}. Ao
instrumentar seu aplicativo móvel com o {{site.data.keyword.amashort}} SDK, é possível exigir que os usuários efetue login para acessar o Node.js ou serviços móveis do {{site.data.keyword.Bluemix_notm}}. Além das capacidades de segurança, o {{site.data.keyword.amashort}} também coleta dados de analítica, de modo que é possível monitorar o desempenho do aplicativo móvel e coletar logs do cliente e estatísticas de uso. </td>
<td valign="top"><b>Provedores de identidade do usuário</b> <br/>É possível usar os provedores de identidade a seguir: <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Ícone do serviço Push Notifications"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>O serviço {{site.data.keyword.mobilepushfull}} fornece uma plataforma unificada para enviar e gerenciar notificações push voltadas para as plataformas iOS e Android. Esse serviço gerencia o mapeamento dos usuários do aplicativo para seus dispositivos, plataforma de dispositivo e manipula o despacho de notificações push para os dispositivos. Com esse serviço, é possível enviar transmissões, unicasts (com base no userID, deviceID) e tags (ou tópicos) com base em notificações push para os usuários do aplicativo móvel.</td>
<td valign="top"><b>Provedores de serviços de push</b><ul><li>Serviço Apple Push Notifications</li><li>Sistema de mensagens em nuvem do Google</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="ícone de serviço do Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant é um NoSQL database as a service (DBaaS). Ele é construído
a partir do zero para escalar globalmente, executar sem interrupção e manipular uma grande variedade de tipos
de dados como JSON, texto completo e geoespacial. </td>
<td>Cloudant.com</td>
</tr>
</table>
