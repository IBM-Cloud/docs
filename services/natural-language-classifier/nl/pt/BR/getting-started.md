---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:download: .download}
{:tip: .tip}

# Iniciar
{: #natural-language-classifier}

O serviço {{site.data.keyword.nlclassifierfull}} pode ajudar seu aplicativo a entender o idioma de textos curtos e fazer predições sobre como manipulá-los. Um classificador aprende com seus dados de exemplo e então pode retornar informações para os textos nos quais ele não está treinado.{:shortdesc}

É possível criar e treinar um {{site.data.keyword.nlclassifiershort}} em menos de 15 minutos.

## Etapa 1: efetue login, crie o serviço e obtenha suas credenciais

Se você já souber suas credenciais para a instância de serviço do {{site.data.keyword.nlclassifiershort}}, ignore esta etapa.
{: tip}

1.  Acesse o [serviço {{site.data.keyword.nlclassifiershort}}](https://console.{DomainName}/catalog/services/natural-language-classifier/) e inscreva-se para uma conta grátis ou efetue login na conta do {{site.data.keyword.Bluemix_notm}}.
1.  Depois de efetuar login, na página {{site.data.keyword.nlclassifiershort}}, digite `Classifier-tutorial` no campo **Nome do serviço** para identificar essa instância do serviço e clique em **Criar**.
1.  Copie suas credenciais:
    1.  Clique em **Credenciais de serviço**.
    2.  Clique em **Visualizar credenciais** na seção "Credenciais de serviço".
    3.  Copie os valores `username` e `password`.

## Etapa 2: crie e treine um classificador
O classificador aprende com exemplos antes que possa retornar informações para os textos que ainda não viu. Os dados de exemplo são referidos como "dados de treinamento". Faça
upload dos dados de treinamento ao criar um classificador.

1.  Faça download da amostra <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>. Esses são os mesmo dados de treinamento usados no [demo ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://natural-language-classifier-demo.mybluemix.net){:new_window}.

	O arquivo está em um formato CSV em duas colunas. A primeira coluna é a entrada de texto. A segunda coluna é a classe para esse texto: temperatura ou condição. Visualize o arquivo para ver as entradas.
2.  Emita o comando curl a seguir para chamar o método `POST /classifiers/`, que faz upload dos dados de treinamento e cria o classificador:
    -   Substitua `{username}` e `{password}` pelas credenciais de serviço copiadas no estágio anterior.
    -   Modifique o local do training\_data para apontar para onde você salvou o arquivo `weather_data_train.csv`.

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	A resposta inclui um novo ID e status de classificador. Por Exemplo:

	```
	{
	  "name": "TutorialClassifier",
	  "language": "en",
	  "status": "Training",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
	  "classifier_id": "10D41B-nlc-1",
	  "created": "2015-05-28T18:01:57.393Z",
	  "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
	}
	```
	{: screen}

	O treinamento começa imediatamente e deve ser concluído antes de ser possível consultar o classificador.
3.  Verifique o status de treinamento periodicamente até que veja um status de `Disponível`. Com esses dados de amostra, o treinamento leva cerca de 6 minutos:
	- Emita uma chamada `GET /classifiers/{classifier_id}` para recuperar o status do classificador. No exemplo a seguir, substitua `{username}`, `{password}` e `{classifier_id}` por suas informações:

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## Etapa 3: classifique texto
Agora que o classificador está treinado, será possível consultá-lo.

1.  Classifique algumas perguntas relacionadas ao clima para revisar como seu classificador recém-treinado responde. Aqui está uma chamada de exemplo. Substitua `{username}`, `{password}` e `{classifier_id}` por suas informações:

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	A API retorna uma resposta que inclui o nome da classe para a qual o classificador tem a confiança mais alta. Outros pares de classe de confiança são listados em ordem decrescente de confiança:

	```
	{
	  "classifier_id": "10D41B-nlc-1",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
	  "text": "How hot will it be today?",
	  "top_class": "temperature",
	  "classes": [
	    {
	      "class_name": "temperature",
	      "confidence": 0.9998201258549781
	    },
	    {
	      "class_name": "conditions",
	      "confidence": 0.00017987414502176904
	    }
	  ]
	}
	```
	{: screen}

	O valor de confiança representa uma porcentagem e valores mais altos representam confianças maiores. A resposta inclui até 10 classes.

	Se você tiver menos de 10 classes nos dados de treinamento, a soma de todos os valores de confiança será 100%. Nestes dados de treinamento de amostra, apenas duas classes são definidas, portanto, apenas duas podem ser retornadas.
2.  Revise a classe principal das perguntas para ver como o classificador as está predizendo.

	Aqui estão algumas outras perguntas de amostra para classificar:

	-   Está quente lá fora?
	-   Será que vai ventar?
	-   Será que veremos sol?
	-   Qual é a máxima esperada para hoje?
	-   Será que teremos nevoeiro amanhã de manhã?

	Uma das perguntas de amostra inclui um termo ("nevoeiro") para o qual o classificador não está treinado. O classificador pode pontuar bem esses termos "omissos" sem ter que fazer trabalho extra para identificá-los. Tente outras perguntas que incluam palavras que não estejam nos dados de treinamento, por exemplo, "granizo" ou "tempestade".

Pronto! Você criou, treinou e consultou um classificador no serviço {{site.data.keyword.nlclassifiershort}}.

## Exclua o classificador do tutorial

Para que seja possível criar classificadores para seu próprio uso e com seus próprios dados de treinamento, talvez você queira excluir esse classificador do tutorial. Para excluir o classificador, chame o método `DELETE /classifiers/{classifier_id}`.

Conforme anteriormente, substitua `{username}`, `{password}` e `{classifier_id}` pelas informações no comando a seguir.

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

A resposta para o comando é um objeto JSON vazio.

## O Que Fazer Depois
Você tem um entendimento básico de como usar o {{site.data.keyword.nlclassifiershort}}. Agora vá além:
- Saiba como [usar seus próprios dados](/docs/natural-language-classifier/using-your-data.html) para treinar um classificador.
- Leia sobre a API na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}.
- Interaja com a API no [explorador de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}.
- Verifique o [aplicativo iniciador Node.js](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window} para obter um app da web de exemplo.
