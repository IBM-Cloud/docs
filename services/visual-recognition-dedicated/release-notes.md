---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="_blank"}

# Release Notes for Visual Recognition Dedicated
The following new features and changes to the service are available.

## 31 March 2017
{: notoc}

This is the General Availability release of the {{site.data.keyword.visualrecognitionshort}} Dedicated service.

Any custom classifiers that were created while the service was in Beta must be recreated in a GA instance of the service.

Please be aware of the following items when using the {{site.data.keyword.visualrecognitionshort}} service:

- **Version date:** To utilize the features of this release, use `2016-05-17` as the value for the `version` parameter.
- **Classes and classifiers:** Single classifiers are called "classes". A group of classes is called a "classifier".
- **Classification:** Use the `POST` or `GET /v3/classify` methods to quickly and accurately identify a variety of subjects and scenes with default classes.
- **Multi-faceted custom classifiers:** You can create and train highly-specialized classifiers that are defined by several classes. For example, you can create a "new\_red\_car" classifier that is defined by the classes "new\_cars" and "red\_cars". To learn more about creating multi-faceted classifiers, see [Structure of the training data](customizing.html#structure).
- **Asynchronous training:** Training of custom classifiers is asynchronous, so training calls complete quickly while your custom classifier continues to learn in the background. To check on the training status of your custom classifier and find out when it is available for use, call the `GET /v3/classifiers/{classifier_id}` method and check the `status` response parameter.
