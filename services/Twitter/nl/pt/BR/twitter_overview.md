---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sobre o {{site.data.keyword.twittershort}}
{: #about_twitter}

*Última atualização: 13 de maio de 2016*
{: .last-updated}

Use {{site.data.keyword.twitterfull}} para incorporar o conteúdo do Twitter
a partir dos fluxos do Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} ou [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} aos aplicativos {{site.data.keyword.Bluemix}}.
{:shortdesc}

O armazenamento de conteúdo é atualizado e indexado em tempo real, tornando as procuras dinâmicas e rápidas. O
			serviço enriquece os tweets com impressão e outros insights para
vários idiomas, com base em algoritmos de processamento de linguagem
natural profundos do [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. O processamento em tempo real dos fluxos de dados do Twitter é totalmente suportado e configurável por meio de um conjunto rico de parâmetros de consulta e palavras-chave. O
{{site.data.keyword.twittershort}}
inclui APIs RESTful que permitem customizar suas procuras e retorna
tweets e enriquecimentos em formato JSON. Tweets
retornados aderem ao formato [Gnip Activity Stream](http://support.gnip.com/sources/twitter/data_format.html){: new_window} para os dados do Twitter.

O serviço {{site.data.keyword.twittershort}} analisa os fluxos do Twitter Decahose e do PowerTrack em tempo real para fornecer os enriquecimentos a seguir para cada autor do tweet:
* Sexo
* Localização permanente (definida por país, estado e cidade)

Os enriquecimentos a seguir também estão disponíveis para o conteúdo de Tweet:

* Impressão (positiva, negativa, ambivalente ou neutra para tweets em inglês, alemão, francês e espanhol)
* Frases de impressão positiva/negativa contidas em um Tweet
(para Tweets em inglês, alemão, francês e espanhol)

Para validar os resultados da procura do
{{site.data.keyword.twittershort}},
o serviço fornece um método de API REST que confirma se um
determinado tweet ainda está acessível no Twitter. 

## Feedback e suporte 
{: #feedback_support}

A equipe
{{site.data.keyword.twitterfull}}
deseja ouvi-lo.

Se você passou por qualquer problema com este serviço, visite o
fórum [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} da IBM. Procure respostas para perguntas enviadas anteriormente ou faça uma pergunta.
Inclua as tags **insights-twitter** e **bluemix** para aprimorar o tempo de resposta.

Se suas perguntas não forem direcionadas no developerWorks Answers, poste-as no
[Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} e identifique sua pergunta com **twitter** e **bluemix**.

Também é possível visualizar o status da [Plataforma Bluemix](https://developer.ibm.com/bluemix/support/#status){: new.window}
ou de [abrir um chamado de suporte](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. Para obter mais informações, consulte  [Resolução de Problemas](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
