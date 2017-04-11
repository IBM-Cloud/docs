---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Creating a custom classifier
{: #custom-classifier}
After you classify an image, you are ready to train and create a custom classifier. With a custom classifier, you can train the {{site.data.keyword.visualrecognitionshort}} Dedicated service to classify images to suit your business needs.
{: shortdesc}

## Step 1: Log in, create the service, and get your credentials
If you created your free instance of the {{site.data.keyword.visualrecognitionshort}} Dedicated service in "Getting started", use those credentials for this tutorial. If you haven't created a service, go back and run through those steps in the beginning of [Getting started](index.html).

## Step 2: Creating a custom classifier
The {{site.data.keyword.visualrecognitionshort}} Dedicated service can learn from example images you upload to create a new, multi-faceted classifier. Each example file is trained against the other files in that call, and positive examples are stored as classes. These classes are grouped to define a single classifier, but return their own scores.

**Note**: Negative example files are not stored as classes.

1.  Download the [beagle.zip ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/beagle.zip){:new_window}, [husky.zip ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/husky.zip){:new_window}, [golden-retriever.zip ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/golden-retriever.zip){:new_window}, and [cats.zip ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/cats.zip){:new_window} example training files.
2.  Call the `POST /v3/classifiers` method with the following cURL command, which uploads the training data and creates the classifier "dogs":
    - Replace `{username}` and `{password}` with the service credentials you copied in the first step.
    - Modify the location of the `{class}_positive_examples` to point to where you saved the .zip files.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" -F "beagle_positive_examples=@beagle.zip" -F "husky_positive_examples=@husky.zip" -F "goldenretriever_positive_examples=@golden-retriever.zip" -F "negative_examples=@cats.zip" -F "name=dogs" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers?version=2016-05-20"
    ```
    {: pre}

	Positive example filenames require the suffix `_positive_examples`. In this example, the filenames are `beagle_positive_examples`, `goldenretriever_positive_examples`, and `husky_positive_examples`. The prefix (beagle, goldenretriever, and husky) is returned as the name of class.

	The response includes a new classifier ID and status, for example:

	<p class="no-copy"></p>
    
    ```json
    {
      "classifier_id": "dogs_1941945966",
      "name": "dogs",
      "owner": "xxxx-xxxxx-xxx-xxxx",
      "status": "training",
      "created": "2016-05-18T21:32:27.752Z",
      "classes": [
        {"class": "husky"},
        {"class": "goldenretriever"},
        {"class": "beagle"}
      ]
    }
    ```
    {: screen}

3.  Check the training status periodically until you see a status of `ready`. Training begins immediately and must finish before you can query the classifier. Replace `{username}`, `{password}`, `{classifier_id}`, and the `https . . .` endpoint with your information:

    ```bash
    curl -X GET -u "{username}:{password}" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-17"
    ```
    {: pre}

## Step 3: Updating an existing custom classifier
You can update an existing {{site.data.keyword.visualrecognitionshort}} Dedicated service custom classifier by adding new classes to an existing classifier, or by adding images to an existing class. Improve on the classifier that you created in step 2 by adding a *Dalmatian* class to the types of dogs which can be classified, and by adding more images of cats to the negative example set for the "dogs" classifier.

### To add new classes to an existing classifier:

1.  Download the [dalmatian.zip ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/dalmatian.zip){:new_window} and [more-cats.zip ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/more-cats.zip){:new_window} sample training files.

2.  Call the `POST /v3/classifiers/{classifier_id}` method with the following cURL command, which uploads the training data and updates the classifier "dogs\_1941945966":
    - Replace `{username}` and `{password}` with the service credentials you copied in the first step.
    - Replace `{classifier_id}` with the ID of the classifier you want to update.
    - Modify the location of the `{class}_positive_examples` to point to where you saved the .zip files.
    - Replace the `https . . .` endpoint with your endpoint URL

    ```bash
    curl -X POST -u "{username}:{password}" -F "dalmatian_positive_examples=@dalmatian.zip" -F "negative_examples=@more-cats.zip" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-17"
    ```
    {: pre}

	The existing "dogs" classifier is replaced by the retrained one with the same `classifier_id`. The response lists the new set of classes and the current status. For example:

	<p class="no-copy"></p>
    
    ```json
    {
      "classifier_id": "dogs_1941945966",
      "name": "dogs",
      "owner": "xxxx-xxxxx-xxx-xxxx",
      "status": "retraining",
      "created": "2016-05-18T21:32:27.752Z",
      "classes": [
        {"class": "dalmatian"},
        {"class": "husky"},
        {"class": "goldenretriever"},
        {"class": "beagle"}
      ]
    }
    ```
    {: screen}

	Training begins immediately. When the new one is available, the status changes to `ready`.

	Don't issue another retraining request until after the current status `ready` state. Multiple requests to retrain a classifier result in a single retraining taking effect. A timestamp called `retrained` shows the last time the classifier retraining completed.

	If you call the `/classify` method while the classifier is retraining, the old definition of the classifier is used.

3.  Check the training status periodically until you see a status of `ready`. Replace `{username}`, `{password}`, `{classifier_id}`, and the `https . . .` endpoint with your information:

    ```bash
    curl -X GET -u "{username}:{password}" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-17"
    ```
    {: pre}

## Step 4: Classifying an image with a custom classifier
When the new classifier completes training, you can call it to see how it performs.

1.  Create a JSON file called `myparams.json` that includes the parameters for your call, such as the `classifier_id` of your new classifier, and the default classifier. A simple JSON file might look like the following:

	<p class="no-copy"></p>
    
    ```json
    {
    "classifier_ids": ["dogs_1941945966", "default"] 
    }
    ```
    {: screen}

2. Use the `POST /v3/classify` method to test your custom classifier. The following example uploads the image [dogs.jpg](https://github.com/watson-developer-cloud/doc-tutorial-downloads/raw/master/visual-recognition/dogs.jpg), and classifies it against the "dogs\_1941945966" classifier.
    - Replace `{username}` and `{password}` with the service credentials you copied in the first step.
    - Replace the `https . . .` endpoint with your endpoint URL
    - To classify against default classes, omit the `parameters` parameter.

    ```bash
    curl -X POST -u "{username}:{password}" -F "images_file=@dogs.jpg" -F "parameters=@myparams.json" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2016-05-17"
    ```
    {: pre}

	The response includes classifiers, their classes, and a score for each class. Scores range from 0-1, with a higher score indicating greater correlation. The `/v3/classify` calls omit low-scoring classes by default if high-scoring classes are identified. You can set a minimum score to display by specifying a floating point value for the `threshold` parameter in your call.

	<p class="no-copy"></p>
    
    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classes": [
                {
                  "class": "animal",
                  "score": 1.0,
                  "type_hierarchy": "/animals"
                },
                {
                  "class": "mammal",
                  "score": 1.0,
                  "type_hierarchy": "/animals/mammal"
                },
                {
                  "class": "dog",
                  "score": 0.880797,
                  "type_hierarchy": "/animals/pets/dog"
                }
              ],
              "classifier_id": "default",
              "name": "default"
            },
            {
              "classes": [
                {
                  "class": "goldenretriever",
                  "score": 0.610501
                }
              ],
              "classifier_id": "dogs_2084675858",
              "name": "dogs"
            }
          ],
          "image": "dogs.jpg"
        }
      ],
      "images_processed": 1
    }
    ```
    {: screen}

3.  Review your results.

You're done! You created, trained, and queried a custom classifier with the {{site.data.keyword.visualrecognitionshort}} service.

## Step 5: Deleting your custom classifier

You might want to delete your custom classifier to begin developing your application with a clean instance.

To delete the classifier, call the `DELETE /v3/classifiers/{classifier_id}` method. Replace `{username}`, `{password}`, and the `https . . .` endpoint with your information. Include the `classifier_id` for the classifier you want to delete:

```bash
curl -X DELETE -u "{username}:{password}" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers/{classifier_id}?version=2016-05-17"
```
{: pre}

### Attributions
{: #attributions}

All images used on this page are from Flikr and used under [Creative Commons Attribution 2.0 license  ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://creativecommons.org/licenses/by/2.0/deed.en){:new_window}. No changes were made to these images.

# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples}

* Learn more about how to [Use your own data to train a classifier](customizing.html).
* Learn more about [Best practices for custom classifiers](https://www.ibm.com/blogs/bluemix/2016/10/watson-visual-recognition-training-best-practices/)