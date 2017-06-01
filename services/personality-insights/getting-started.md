---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"

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
{: #gettingstarted}

{{site.data.keyword.personalityinsightsfull}} allows applications to derive insights about personality characteristics from social media, enterprise data, or other digital communications. This tutorial shows you how to call the `POST profile` method with different types of input and return different types of output and output formats.
{: shortdesc}

## Step 1: Log in, create the service, and get your credentials
{: #create-service}

If you already know your credentials for the {{site.data.keyword.personalityinsightsshort}} service instance, skip this step.
{: tip}

1.  Go to the [{{site.data.keyword.personalityinsightsshort}} service](https://console.{DomainName}/catalog/services/personality-insights/) and either sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
1.  After you log in, type `personality-tutorial` in the **Service name** field of the {{site.data.keyword.personalityinsightsshort}} page. Click **Create**.
1.  Copy your credentials:
    1.  Click **Service credentials**.
    1.  Click **View credentials** under **Actions**.
    1.  Copy the `username` and `password` values.

## Step 2: Send plain text and receive basic JSON output
{: #example1}

The first example passes a plain text file to the `profile` method and implicitly requests the default JSON response. The example uses the `charset` parameter with the **Content-Type** header to specify the character encoding of the input text.

1.  Download the sample <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/personality-insights/profile.txt" download="profile.txt">profile.txt</a> file.
1.  Issue the following command to send the file to the `profile` method and implicitly request the default JSON response. The `charset` parameter with the **Content-Type** header specifies the character encoding of the input text:
    - Replace `{username}` and `{password}` with the service credentials you copied in the previous step.
    - Modify the location of `{path_to_file}` to point to where you saved the `profile.txt` file.

      ```bash
      curl -X POST --user "{username}":"{password}" \
      --header "Content-Type: text/plain;charset=utf-8" \
      --data-binary "@{path_to_file}/profile.txt" \
      "https://gateway.watsonplatform.net/personality-insights/api/v3/profile?version=2016-10-20"
      ```
      {: pre}

    The service returns a JSON profile that includes information about the Big Five personality, Needs, and Values characteristics for the author as inferred from the input text. The `percentile` returned for each characteristic reports the author's normalized score for that characteristic. The service computes the percentile by comparing the author's results with the results from a sample population.

    The service also reports basic metadata, such as the number of words in the input, the language model with which the input was processed, and any warnings associated with the input.

    ```javascript
    {
      "word_count": 1365,
      "processed_language": "en",
      "personality": [
        {
          "trait_id": "big5_openness",
          "name": "Openness",
          "category": "personality",
          "percentile": 0.99708142449829,
          "children": [
            {
              "trait_id": "facet_adventurousness",
              "name": "Adventurousness",
              "category": "personality",
              "percentile": 0.78974535615104
            },
            . . .
          ]
        },
        {
          "trait_id": "big5_conscientiousness",
          "name": "Conscientiousness",
          "category": "personality",
          "percentile": 0.81001753184176,
          "raw_score": 0.66899984888815,
          "children": [
            {
              "trait_id": "facet_achievement_striving",
              "name": "Achievement striving",
              "category": "personality",
              "percentile": 0.84613299226628,
              "raw_score": 0.74240118454888
            },
            . . .
          ]
        },
        {
          "trait_id": "big5_extraversion",
          "name": "Extraversion",
          "category": "personality",
          "percentile": 0.085300585565483,
          "children": [
            {
              "trait_id": "facet_activity_level",
              "name": "Activity level",
              "category": "personality",
              "percentile": 0.96240163134159
            },
            . . .
          ]
        },
        {
          "trait_id": "big5_agreeableness",
          "name": "Agreeableness",
          "category": "personality",
          "percentile": 0.18753528603195,
          "children": [
            {
              "trait_id": "facet_altruism",
              "name": "Altruism",
              "category": "personality",
              "percentile": 0.97133020063318
            },
            . . .
          ]
        },
        {
          "trait_id": "big5_neuroticism",
          "name": "Emotional range",
          "category": "personality",
          "percentile": 0.94385641645805,
          "children": [
            {
              "trait_id": "facet_anger",
              "name": "Fiery",
              "category": "personality",
              "percentile": 0.013938100678609
            },
            . . .
          ]
        }
      ],
      "needs": [
        {
          "trait_id": "need_challenge",
          "name": "Challenge",
          "category": "needs",
          "percentile": 0.003254653691494
        },
        {
          "trait_id": "need_closeness",
          "name": "Closeness",
          "category": "needs",
          "percentile": 0.37022781101807
        },
        . . .
      ],
      "values": [
        {
          "trait_id": "value_conservation",
          "name": "Conservation",
          "category": "values",
          "percentile": 0.50659292186185
        },
        {
          "trait_id": "value_openness_to_change",
          "name": "Openness to change",
          "category": "values",
          "percentile": 0.62875169494626
        },
        . . .
      ],
      "warnings": []
    }
    ```
    {: codeblock}

## Step 3: Send JSON input and receive detailed JSON output
{: #example2}

The second example passes JSON content, again accepting the default JSON response. The `consumption_preferences` and `raw_scores` query parameters are set to `true` to request a more detailed analysis of the input.

1.  Download the sample <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/personality-insights/profile.json" download="profile.json">profile.json</a> file.
1.  Issue the following command to send the JSON file. Unlike the first example, the `charset` parameter is not needed with the **Content-Type** header for JSON input.
    - Replace `{username}` and `{password}` with your information.
    - Modify the location of `{path_to_file}` to point to where you saved the `profile.json` file.

      ```bash
      curl -X POST --user "{username}":"{password}" \
      --header "Content-Type: application/json" \
      --data-binary "@{path_to_file}/profile.json" \
      "https://gateway.watsonplatform.net/personality-insights/api/v3/profile?version=2016-10-20&consumption_preferences=true&raw_scores=true"
      ```
      {: pre}

    The service returns a JSON profile that includes the characteristics and metadata returned with the first example. For each characteristic, the service also includes a `raw_score`, which represents the author's score for the characteristic based solely on the input text, without comparing the results to a sample population.

    Because the input content includes timestamps, the service also reports behavioral characteristics. These are temporal characteristics that indicate the `percentage` of the content items that were created each day of the week and hour of the day.

    The service also reports a `score` for a collection of consumption preferences. For each preference, the service provides a `score` that indicates the author's likelihood to prefer different products, services, and activities based on the inferred characteristics.

    ```javascript
    {
      "word_count": 15223,
      "processed_language": "en",
      "personality": [
        {
          "trait_id": "big5_openness",
          "name": "Openness",
          "category": "personality",
          "percentile": 0.8011555009553,
          "raw_score": 0.77565404255038,
          "children": [
            . . .
          ]
        },
        {
          "trait_id": "big5_conscientiousness",
          "name": "Conscientiousness",
          "category": "personality",
          "percentile": 0.81001753184176,
          "raw_score": 0.66899984888815,
          "children": [
            . . .
          ]
        },
        {
          "trait_id": "big5_extraversion",
          "name": "Extraversion",
          "category": "personality",
          "percentile": 0.64980796071382,
          "raw_score": 0.56817738781166,
          "children": [
            . . .
          ]
        },
        {
          "trait_id": "big5_agreeableness",
          "name": "Agreeableness",
          "category": "personality",
          "percentile": 0.94786124793821,
          "raw_score": 0.80677815631809,
          "children": [
            . . .
          ]
        },
        {
          "trait_id": "big5_neuroticism",
          "name": "Emotional range",
          "category": "personality",
          "percentile": 0.5008224041628,
          "raw_score": 0.46748200007024,
          "children": [
            . . .
          ]
        }
      ],
      "needs": [
        {
          "trait_id": "need_challenge",
          "name": "Challenge",
          "category": "needs",
          "percentile": 0.67362332054511,
          "raw_score": 0.75196348037675
        },
        . . .
      ],
      "values": [
        {
          "trait_id": "value_conservation",
          "name": "Conservation",
          "category": "values",
          "percentile": 0.89268222856139,
          "raw_score": 0.72135308187423
        },
        . . .
      ],
      "behavior": [
        {
          "trait_id": "behavior_sunday",
          "name": "Sunday",
          "category": "behavior",
          "percentage": 0.21392532795156
        },
        . . .
        {
          "trait_id": "behavior_saturday",
          "name": "Saturday",
          "category": "behavior",
          "percentage": 0.077699293642785
        },
        {
          "trait_id": "behavior_0000",
          "name": "0:00 am",
          "category": "behavior",
          "percentage": 0.4561049445005
        },
        . . .
        {
          "trait_id": "behavior_2300",
          "name": "11:00 pm",
          "category": "behavior",
          "percentage": 0.12310797174571
        }
      ],
      "consumption_preferences": [
        {
          "consumption_preference_category_id": "consumption_preferences_shopping",
          "name": "Purchasing Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_automobile_ownership_cost",
              "name": "Likely to be sensitive to ownership cost when buying automobiles",
              "score": 0
            },
            . . .
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_health_and_activity",
          "name": "Health & Activity Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_eat_out",
              "name": "Likely to eat out frequently",
              "score": 1
            },
            . . .
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_environmental_concern",
          "name": "Environmental Concern Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_concerned_environment",
              "name": "Likely to be concerned about the environment",
              "score": 0
            }
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_entrepreneurship",
          "name": "Entrepreneurship Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_start_business",
              "name": "Likely to consider starting a business in next few years",
              "score": 1
            }
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_movie",
          "name": "Movie Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_movie_romance",
              "name": "Likely to like romance movies",
              "score": 1
            },
            . . .
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_music",
          "name": "Music Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_music_rap",
              "name": "Likely to like rap music",
              "score": 1
            },
            . . .
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_reading",
          "name": "Reading Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_read_frequency",
              "name": "Likely to read often",
              "score": 0
            },
            . . .
          ]
        },
        {
          "consumption_preference_category_id": "consumption_preferences_volunteering",
          "name": "Volunteering Preferences",
          "consumption_preferences": [
            {
              "consumption_preference_id": "consumption_preferences_volunteer",
              "name": "Likely to volunteer for social causes",
              "score": 0
            },
            . . .
          ]
        }
      ],
      "warnings": []
    }
    ```
    {: codeblock}

## Step 4: Send JSON input and receive detailed CSV output
{: #example3}

This third example is similar to the second: it passes the same JSON content and requests the same results. But this example specifies `text/csv` for the **Accept** header to request the response in comma-separated values (CSV) format, using the `--output` option of the curl command to direct the results to a file named `profile.csv`. The example also sets the `csv_headers` query parameter to `true` to request that column headers be returned with the output.

1.  Issue the following command to send the json file:
    - Replace `{username}` and `{password}` with your information.
    - Modify the location of `{path_to_file}` to point to where you saved the `profile.json` file.

      ```bash
      curl -X POST --user "{username}":"{password}" \
      --header "Content-Type: application/json" \
      --header "Accept: text/csv" \
      --data-binary "@{path_to_file}/profile.json" \
      --output profile.csv \
      "https://gateway.watsonplatform.net/personality-insights/api/v3/profile?version=2016-10-20&consumption_preferences=true&raw_scores=true&csv_headers=true"
      ```
      {: pre}

For a detailed description of the CSV response and headers, see [CSV response content ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/personality-insights/output.html#outputCSV).

You're done! You used the {{site.data.keyword.personalityinsightsshort}} to analyze both plain text and JSON content and set different output types and formats.

## Next steps
{: #next-steps}

- Learn about the Big Five [personality model ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/personality-insights/models.html){:new_window}.
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}.
- Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}.
- Look at the [Node.js sample app ![External link icon](../../icons/launch-glyph.svg "External link icon")]((https://github.com/watson-developer-cloud/personality-insights-nodejs){:new_window} for an example web app.
