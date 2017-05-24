---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Managing classifiers with the toolkit
{: #managing-toolkit}

You can manage your training data and classifiers by using the {{site.data.keyword.nlclassifierfull}} Toolkit web application. The toolkit gives you a unified view of all the classifiers that are running in the same {{site.data.keyword.Bluemix_notm}} service instance.
{: shortdesc}

This is a beta release of the toolkit. The beta version of this toolkit might not be supported after a new release or after the toolkit exits beta status. Do not use the toolkit for production use.

The web interface of the toolkit simplifies how you train and test a classifier. Your domain experts can use the toolkit to focus on the quality of your training data.

## Getting access
{: #getting-access}

You can find a link to the toolkit on the {{site.data.keyword.Bluemix_notm}} service dashboard page for your instance of {{site.data.keyword.nlclassifiershort}}.

### Accessing the toolkit yourself

To find the link to the toolkit, follow these steps to get to your {{site.data.keyword.Bluemix_notm}} **service** dashboard:

1.  Open your {{site.data.keyword.nlclassifiershort}} service tile by logging into your [{{site.data.keyword.Bluemix_notm}} Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/dashboard/services){: new_window}.

    - In the **Services** area, click your {{site.data.keyword.nlclassifiershort}} service tile to open the instance dashboard. (If you don't have a service tile, [create an instance ![External link icon](../../icons/launch-glyph.svg)](https://console.{DomainName}/catalog/services/natural-language-classifier/){: new_window} of the {{site.data.keyword.nlclassifiershort}} service.)
1.  In the service dashboard, click **Access the beta toolkit**.

    Bookmark the URL for easy access to the toolkit later.
    {: tip}

### Giving access to your toolkit to others

You can allow others to use your toolkit by adding them in {{site.data.keyword.Bluemix_notm}}.

1.  In {{site.data.keyword.Bluemix_notm}}, click **Account > Invite Team Members**.
1.  Select the org that holds your classifier service and click **Next**.
1.  Select the space that holds your classifier service.
1.  Select the **Developer** space role. For details about roles, see [Managing team members and roles](/docs/admin/users_roles.html).
1.  Enter the user's email address and click **Send**.
1.  In a separate email, send the URL of your toolkit (that you bookmarked earlier) to the users.

## Example uses
{: #example-uses}

In these examples, you create and modify training data, test a classifier interactively or from a set of test data, and update training data from the results.

### Create training data in the toolkit

Get familiar with the {{site.data.keyword.nlclassifiershort}} toolkit by creating a small set of training data with the toolkit.

Before you can create a classifier, you need training data. You can create the data by typing texts and classes, or you can upload your training data from a CSV file that matches the [file format](/docs/services/natural-language-classifier/using-your-data.html).

1.  On the **Training data** page of the toolkit, add a text. If you can't think of one, add, `Where is the nearest ATM`.
1.  Assign a class to the text by typing it in. For the ATM example, type `location`.
1.  Continue adding texts and classes to your training data. You can assign classes to texts in the following ways:
    - Select a class by clicking it, and then click **Add text**. Or select a text, and then click **Assign classes**.
    - Select a class, then drag a text to it. Or select a text, and then drag a class to it.

    You can work on more than one class or text at a time by pressing Ctrl and clicking the text or class (press Command on a Mac). Try them out.
1.  After you worked with your training data for a while, click **Download training data** to save the data as a backup.
    You can also upload this file to the toolkit to work with the training data again later.
    {: tip}
1.  When you've assigned classes to at least five texts, you can create a classifier from this training data. Click **Create classifier**. {{site.data.keyword.watson}} starts training the classifier.

### Test your classifier and update your training data

After a classifier is trained and available, you can check how well it classifies texts that it hasn't seen before. You can test a series of texts and improve the training data by adding the incorrect or low confidence responses.

1.  On the **Classifiers** page, click **Test and improve performance** for the classifier that you want to test.
1.  On the **Improve performance** page, enter a text that is not in your training data and click **Classify**. {{site.data.keyword.watson}} returns relevant classes and their confidence levels.
1.  Add more texts to test the performance.
1.  Review the responses. Flag or approve the results that you want to add to your training data:
    - If the classification is not correct, flag the result.
    - If the response is correct but the confidence is low, add it to your training data by clicking **Approve**.
1.  Click **Add to training data** to add the approved and flagged responses to your training data.
1.  On the **Training data** page, review and update the classes that are assigned to the texts that you flagged.
1.  To update your classifier with this new training data, you'll create another one. Click **Create classifier**. After it is trained, test the new classifier to see how it improved.

### Upload data to test your classifier

Entering texts to classify one by one is effective for quick tests. However if you have a *test set*, you can upload the set to the toolkit to classify many at the same time. A test set is a group of example texts that are not in your training data,. You use the set to check the performance of the classifier.

1.  Create a test set file:
    - The file can use the same format as the training data (in other words, it can include the correct classes) or include only texts, one on each line. Make sure that the texts (and classes) adhere to the [file format](/docs/services/natural-language-classifier/using-your-data.html) requirements.
    - Save the file with a `.csv` extension.
1.  On the **Classifiers** page, click **Test and improve performance** for the classifier that you want to test.
1.  On the **Improve performance** page, click **Use test data**. {{site.data.keyword.watson}} uploads the data, classifies each text, and returns a response.
1.  Compare the responses against the correct classification and also look for low confidence.
1.  Improve the training data by adding more examples. Don't add examples that exist in your test set if you want to continue to use it to assess the performance of the classifier.
