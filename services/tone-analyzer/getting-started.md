---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Getting started tutorial
{: #getting started}

You use {{site.data.keyword.toneanalyzerfull}} to understand conversations and communications. This tutorial guides you through using {{site.data.keyword.toneanalyzershort}} to analyze some sample content, and then for your own content. You'll also learn how to analyze customer support interactions.
{: shortdesc}

## Step 1: Log in, create the service instance, and get your credentials
{: #create-service}

If you already know your credentials for the {{site.data.keyword.toneanalyzershort}} service instance, skip this step.
{: tip}

1.  Go to the [{{site.data.keyword.toneanalyzershort}} service](https://console.{DomainName}/catalog/services/tone-analyzer/) and either sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
1.  After you log in, type `tone-tutorial` in the **Service name** field of the {{site.data.keyword.toneanalyzershort}} page. Click **Create**.
1.  Copy your credentials:
    1.  Click **Service credentials**.
    1.  Click **View credentials** under **Actions**.
    1.  Copy the `username` and `password` values.

## Step 2: Analyze some sample content

1.  Issue this command to call the `POST /v3/tone-analyzer` method, which analyzes the sample JSON content. Replace `{username}` and `{password}` with the service credentials you copied in the previous step:

    ```bash
    curl --user "{username}":"{password}" \
    --header "Content-Type: application/json" \
    --data  "{\"text\": \"Hi Team, I know the times are difficult! Our sales have been disappointing for the past three quarters for our data analytics product suite. We have a competitive data analytics product suite in the industry. But we need to do our job selling it! \"}" \
    "https://gateway.watsonplatform.net/tone-analyzer/api/v3/tone?version=2016-05-19"
    ```
    {: pre}

1.  Limit the results to see only the "emotion" tone by including the **tones** parameter set to `emotion`:

    ```bash
    curl --user "{username}":"{password}" \
    --header "Content-Type: application/json" \
    --data "{\"text\": \"Hi Team, I know the times are difficult! Our sales have been disappointing for the past three quarters for our data analytics product suite. We have a competitive data analytics product suite in the industry. But we need to do our job selling it! \"}" \
    "https://gateway.watsonplatform.net/tone-analyzer/api/v3/tone?version=2016-05-19&tones=emotion"
    ```
    {: pre}

    You can also set the **tones** parameter to `writing` and `social`. For example, set `tones=emotion,writing` to see only the emotion and writing results.
    {: tip}
1.  Now set the **sentences** parameter to `false` to see an analysis of the entire content instead of sentence-level:

    ```bash
    curl --user "{username}":"{password}" \
    --header "Content-Type: application/json" \
    --data  "{\"text\": \"Hi Team, I know the times are difficult! Our sales have been disappointing for the past three quarters for our data analytics product suite. We have a competitive data analytics product suite in the industry. But we need to do our job selling it! \"}" \
    "https://gateway.watsonplatform.net/tone-analyzer/api/v3/tone?version=2016-05-19&sentences=false"
    ```
    {: pre}

## Step 3: Analyze your own content

- Try the previous commands with your own content in plain text, HTML, or JSON formats. {{site.data.keyword.toneanalyzershort}} supports up to 128KB of text, which is about 1000 sentences.

    Change the **Content-Type** value in the commands to match your input. Valid values are `application/json`, `text/html`, and `plain/text`. For example, `"Content-Type: text/html"`

## Step 4: Analyze content with the customer engagement endpoint

- Issue this command to call the `POST /v3/tone_chat` method, which accepts JSON content:
    - Replace `{username}` and `{password}` with your information.
    - You can replace the `{text}` JSON object with your own escaped text:

      ```bash
      curl --user "{username}":"{password}" \
      --header "Content-Type: application/json" \
      --data '{"utterances": [{"text": "Hello, can you help me", "user": "customer"}, {"text": "How are you ?", "user": "agent"}, {"text": "Nothing is working :(", "user": "customer"}, {"text": "Sorry to hear this", "user": "agent"}]}' \
      "https://gateway.watsonplatform.net/tone-analyzer/api/v3/tone_chat?version=2016-05-19"
      ```
      {: pre}

You're done! You analyzed both general purpose and customer support content with {{site.data.keyword.toneanalyzershort}}.

## Next steps
{: #next-steps}

You have a basic understanding of how to use {{site.data.keyword.toneanalyzershort}}. Now dive deeper:

- Learn about the [tone score ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/tone-analyzer/understand-tone.html){:new_window}
- Get inspired by reading the [case studies ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/tone-analyzer/case-studies.html){:new_window}
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/tone-analyzer/api/){:new_window}
- Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.mybluemix.net/apis/tone-analyzer-v3){:new_window}