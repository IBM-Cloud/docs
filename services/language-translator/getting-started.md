---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"

---
<!-- Attribute definitions -->
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Getting started tutorial
{: #gettingstarted}

{{site.data.keyword.languagetranslatorfull}} allows you to programmatically translate text in news, conversational, and patent domains. This tutorial walks you through the commands to translate some sample content from English to Spanish and to choose the domain.
{:shortdesc}

## Step 1: Log in, create the service instance, and get your credentials
{: #create-service}

If you already know your credentials for the {{site.data.keyword.languagetranslatorshort}} service instance, skip this step.
{: tip}

1.  Go to the [{{site.data.keyword.languagetranslatorshort}} service](https://console.{DomainName}/catalog/services/natural-language-classifier/) and either sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
1.  After you log in, type `language-tutorial` in the **Service name** field of the {{site.data.keyword.languagetranslatorshort}} page. Click **Create**.
1.  Copy your credentials:
    1.  Click **Service credentials**.
    1.  Click **View credentials** under **Actions**.
    1.  Copy the `username` and `password` values.

## Step 2: Translate text
{: #translate-text}

Use the following example to translate "Hello, world!" from English to Spanish. Replace `{username}` and `{password}` with the service credentials you copied in the previous step.

```bash
curl -X POST --user "{username}":"{password}" \
--header "Content-Type: application/json" \
--header "Accept: application/json" \
--data '{"text":"Hello, world!","source":"en","target":"es"}' \
"https://gateway.watsonplatform.net/language-translator/api/v2/translate"
```
{:codeblock}

<!-- ```
var watson = require('watson-developer-cloud');
var language_translator = watson.language_translator({
  username: 'username',
  password: 'password',
  version: 'v2',
  url: 'https://gateway.watsonplatform.net/language-translator/api'
});
language_translator.translate({
    text: 'Hello, world!',
    source: 'en',
    target: 'es'
  },
  function(err, translation) {
    if (err)
      console.log(err)
    else
      console.log(translation);
});
```
{:node}
{:codeblock} -->

<!-- ```java
LanguageTranslator service = new LanguageTranslator();
service.setUsernameAndPassword("username","password");

TranslationResult result = service.translate("Hello, world!", "en", "es");
System.out.println(result);
```
{:java}
{:codeblock} -->

<!-- ```
import json
from watson_developer_cloud import LanguageTranslatorV2 as LanguageTranslator

language_translator = LanguageTranslator(
    username="username",
    password="password")

translation = language_translator.translate(
    text="Hello, world!",
    source="en",
    target="es"
print(json.dumps(translation, indent=2, ensure_ascii=False))
```
{:python}
{:codeblock} -->


## Step 3: Try a domain-specific model
{: #specify-model}

{{site.data.keyword.languagetranslatorshort}} has specialized models for news, conversational, and patent domains. When you specify `source` and `target` languages as in Step 2, the service usually defaults to the news domain model for that translation path. To use a domain-specific model, specify the `model_id` instead of the `source` and `target` languages. You can also use a [custom model](https://www.ibm.com/watson/developercloud/doc/language-translator/customizing.html){: new_window} if you created one.

The following example translates "Hey world, whats up?" with the English-to-Spanish conversational model. Replace `{username}` and `{password}` with your information:

```bash
curl -X POST --user "{username}":"{password}" \
--header "Content-Type: application/json" \
--header "Accept: application/json" \
--data '{"text":"Hey world, whats up?","model_id":"en-es-conversational"}' \
"https://gateway.watsonplatform.net/language-translator/api/v2/translate"
```
{:codeblock}

<!-- ```
var watson = require('watson-developer-cloud');
var language_translator = watson.language_translator({
  username: 'username',
  password: 'password',
  url: 'https://gateway.watsonplatform.net/language-translator/api'
  version: 'v2',
});
language_translator.translate({
    text: 'Hey, world! What's up?',
    model_id: 'en-es-conversational'
  },
  function(err, translation) {
    if (err)
      console.log(err)
    else
      console.log(translation);
});
```
{:node}
{:codeblock} -->

<!-- ```java
LanguageTranslator service = new LanguageTranslator();
service.setUsernameAndPassword("username","password");

TranslationResult result = service.translate("Hey, world! What's up?", "en-es-conversational");
System.out.println(result);
```
{:java}
{:codeblock} -->

<!-- ```python
import json
from watson_developer_cloud import LanguageTranslatorV2 as LanguageTranslator

language_translator = LanguageTranslator(
  username="username",
  password="password"
)

translation = language_translator.translate(
  text="Hey, world! What's up?",
  model_id="en-es-conversational"
)
print(json.dumps(translation, indent=2, ensure_ascii=False))
```
{:python}
{:codeblock} -->

You can use the [List models ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/language-translator/api/v2/?python#list-models){: new_window} method to view the available models for your service instance.
{:tip}

## Next steps
{: #next-steps}

- Learn how to [customize ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/language-translator/customizing.html){: new_window} {{site.data.keyword.languagetranslatorshort}} to work for your use case.
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}.
- Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}.
- Look at the [Node.js sample app ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/language-translator-nodejs){:new_window} for an example web app.
