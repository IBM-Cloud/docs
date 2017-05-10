---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote do Tradutor do Watson
{: #openwhisk_catalog_watson_translator}

O pacote `/whisk.system/watson-translator` oferece uma maneira conveniente de chamar APIs do Watson para traduzir.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | pacote | username, password | Pacote para tradução de texto e identificação de idioma  |
| `/whisk.system/watson-translator/translator` | ação | payload, translateFrom, translateTo, translateParam, username, password | Traduzir texto |
| `/whisk.system/watson-translator/languageId` | ação | payload, username, password | Identificar idioma |

**Nota**: o pacote `/whisk.system/watson` está descontinuado, incluindo as ações `/whisk.system/watson/translate` e `/whisk.system/watson/languageId`.

## Configurando o pacote do Tradutor do Watson no Bluemix

Se você estiver usando o OpenWhisk a partir do Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Watson
do Bluemix.

1. Crie uma instância de serviço do Tradutor do Watson em seu [painel](http://console.ng.Bluemix.net) do Bluemix.
  
  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.
  
2. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Watson que você criou.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  
  
## Configurando um pacote do Tradutor do Watson fora do Bluemix

Se você não estiver usando o OpenWhisk no Bluemix ou se desejar configurar o seu Tradutor do Watson fora do Bluemix, deverá criar manualmente uma ligação de
pacote para o seu serviço de Tradutor do Watson. Você precisa do nome do usuário e da senha do serviço de Tradutor do Watson.

- Crie uma ligação de pacote que esteja configurada para o seu serviço de Tradutor do Watson.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## Traduzindo texto

A ação `/whisk.system/watson-translator/translator` traduz o texto de um idioma para outro. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto a ser traduzido.
- `translateParam`: o parâmetro de entrada indicando o texto a
ser traduzido. Por exemplo, se `translateParam=payload`, o valor do
parâmetro `payload` que é passado à ação será traduzido.
- `translateFrom`: um código de dois dígitos do idioma de origem.
- `translateTo`: um código de dois dígitos do idioma de destino.

- Chame a ação `translator` em sua ligação de pacote para traduzir algum texto do inglês para o francês.
  
  ```
  wsk action invoke myWatsonTranslator/translator \
  --blocking --result \
  --param payload "Blue skies ahead" --param translateFrom "en" \
  --param translateTo "fr"
  ```
  {: pre}
  ```json
     {
      "payload": "Ciel bleu a venir"
  }
  ```
  
  
## Identificando o idioma de algum texto

A ação `/whisk.system/watson-translator/languageId` identifica o idioma de algum texto. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto para identificar.

- Chame a ação `languageId` em sua ligação do pacote para identificar o idioma.
  
  ```
  wsk action invoke myWatsonTranslator/languageId \
  --blocking --result \
  --param payload "Ciel bleu a venir"
  ```
  {: pre}
  ```json
     {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  
