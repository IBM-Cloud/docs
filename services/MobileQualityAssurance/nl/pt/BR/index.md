---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Introdução ao {{site.data.keyword.mqa}} (descontinuado)
{: #gettingstartedtemplate}

**O serviço {{site.data.keyword.mqafull}} foi descontinuado.** Para obter mais informações sobre o status e as datas, consulte, [a entrada de blog Aposentadoria do Bluemix Mobile Quality Assurance ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}. {:deprecated}

O {{site.data.keyword.mqafull}} capacita as equipes a capturar experiência de testador e de usuário em tempo real para construir e entregar continuamente apps móveis de alta qualidade.
{: shortdesc}

Para deixar o serviço {{site.data.keyword.mqa}} funcionando rapidamente, siga estas etapas:

1. Após você criar uma instância <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->do serviço {{site.data.keyword.mqa}}, será possível acessar o Console do {{site.data.keyword.mqa}} clicando em seu tile na seção **Serviços** do Painel do {{site.data.keyword.Bluemix}}.

	O serviço {{site.data.keyword.mqa}} é ativado.

2. Inclua um app móvel na instância do {{site.data.keyword.mqa}} selecionando **Incluir app MQA** e fornecendo um nome para o app.

3. Faça download dos {{site.data.keyword.mqa}} [SDKs clientes ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} e conclua a instrumentação do seu app continuando com um dos procedimentos a seguir:

	* [Instrumentar MQA com um app Android](mqa_inst_app_android.html)
	* [Instrumentar MQA com um app iOS](mqa_inst_app_ios.html)
	* [Instrumentar MQA com um app Cordova](mqa_inst_app_cord.html)

	Um único SDK é usado para instrumentar ambos os apps, de pré-produção e produção. É possível usar o parâmetro `MODE:` para especificar *QA* para o modo de pré-produção ou especificar *MARKET* para o modo de produção. Especifique o modo de pré-produção para que testadores internos possam fornecer informações detalhadas sobre erros e travamentos que ocorrem com seu app. Especifique o modo de produção para que os usuários possam fornecer informações detalhadas sobre seu app. Se seu app estiver em produção, o {{site.data.keyword.mqa}} facilitará a obtenção de feedback de usuários de dentro do app. 

4. Depois de ter instrumentado seu app, é possível visualizar informações de qualidade mais detalhadas para ele selecionando uma das opções a seguir na interface de sua instância de serviço {{site.data.keyword.mqa}}:

	<dl>
		<dt><strong>Sessões</strong></dt>
		<dd>Revise as informações sobre travamentos, erros, feedback e o estado do dispositivo durante a sessão.  Consulte [Visualizando detalhes ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window} no IBM Knowledge Center para obter mais informações.</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Travamentos</strong></dt>
		<dd>Revise informações sobre o que ocorreu para causar travamentos. Consulte [Relatórios de travamento ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window} no IBM Knowledge Center para obter mais informações.</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Erros</strong></dt>
		<dd>Revise informações relatadas por usuários, tais como relatórios de erros, capturas de telas e detalhes do dispositivo. Consulte [Relatórios de erro ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window} no IBM Knowledge Center para obter mais informações.</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Feedback</strong></dt>
		<dd>Revise respostas de feedback do usuário para ver quem escreveu o feedback e quando ele foi escrito. Consulte [Feedback do usuário ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window} no IBM Knowledge Center para obter mais informações.</dd>
		<dt><strong>Pontuação da impressão (se configurada)</strong></dt>
		<dd>Revise a pontuação da impressão do usuário ao longo do tempo e as versões para monitorar, medir e melhorar a qualidade do app. Consulte [Impressão do usuário ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window} no IBM Knowledge Center para obter mais informações.</dd>
		<dt><strong>Dispositivos registrados</strong></dt>
		<dd>Revise a lista de dispositivos usados durante uma sessão de teste e informações sobre esses dispositivos. Consulte [Visualizando informações sobre o dispositivo ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window} no IBM Knowledge Center para obter mais informações.</dd>
	</dl>

	Essas métricas incluem os dados a seguir:

	* Dados de pré-produção para travamentos, erros, feedback e sessões.
	* Dados de produção para travamentos, feedback, impressão e sessões.

	![Captura de tela da interface na qual é possível visualizar métricas de qualidade para um app.](images/quality_metrics_saas4.gif)

	Pela visualização dessas informações de seus apps, será possível determinar se deve investigar problemas mais específicos. Por exemplo, se a taxa de travamento de um app aumentar, será possível clicar na taxa de travamento para visualizar informações mais detalhadas sobre relatórios de travamento desse app.

5. Para visualizar a pontuação geral de impressão para o app, deve-se configurar a análise de impressão:

	1. Na seção *Pontuação de impressão*, clique no link para configurar a análise de impressão para o app selecionado.

	2. Na página Detalhes do Aplicativo, [configure a análise de sentimentos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} e salve suas alterações.


# Links relacionados
{: #rellinks notoc}

## Tutoriais e amostras
{: #samples notoc}

* [Vídeo: Introdução ao Mobile Quality Assurance no Bluemix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [Vídeo: Análise de sentimentos no Mobile Quality Assurance ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: Incluir o IBM Mobile Quality Assurance em seu regime de qualidade móvel ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Criar apps móveis que funcionam: cinco dicas de um painel de especialista ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Criar um app móvel que não é perfeito ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: DevOps para desafios e melhores práticas de apps móveis ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Amostra: bluelist-mqa ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
