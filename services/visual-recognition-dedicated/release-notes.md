---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-19"

---

{:new_window: target="_blank"}

# Release Notes for Visual Recognition Dedicated
The following new features and changes to the service are available.

## 21 April 2017
{: notoc}

This is the General Availability release of the {{site.data.keyword.visualrecognitionshort}} Dedicated service.

Any custom classifiers that were created while the service was in Beta must be recreated in a GA instance of the service.

Please be aware of the following items when using the {{site.data.keyword.visualrecognitionshort}} service:

- **Version date:** To utilize the features of this release, use `2016-05-17` as the value for the `version` parameter.
- **Classes and classifiers:** Single classifiers are called "classes". A group of classes is called a "classifier".
- **Classification:** Use the `POST` or `GET /v3/classify` methods to quickly and accurately identify a variety of subjects and scenes with default classes.
- **Multi-faceted custom classifiers:** You can create and train highly-specialized classifiers that are defined by several classes. For example, you can create a "new\_red\_car" classifier that is defined by the classes "new\_cars" and "red\_cars". To learn more about creating multi-faceted classifiers, see [Structure of the training data](customizing.html#structure).
- **Asynchronous training:** Training of custom classifiers is asynchronous, so training calls complete quickly while your custom classifier continues to learn in the background. To check on the training status of your custom classifier and find out when it is available for use, call the `GET /v3/classifiers/{classifier_id}` method and check the `status` response parameter.
- **`GET` calls for deleted classfiers:** Calling `GET /classifiers` to get a list of active custom classifiers can provide inaccurate results after classifiers have been deleted.  The list of classifiers in the response can include classifiers that have been deleted in the past, and repeated calls will return different results. To work around this issue, check each classifier in the response using `GET /classifiers/{classifier_id}` to learn which are available and which have been deleted.  Making this call for a classifier which has been deleted will result in an error message that the classifier is not found.
- **Repeated calls may stop training job:** Repeatedly calling `GET /classifiers` while training or retraining is in progress, in order to check status, can result in killing the training job. To work around this issue, poll a new classifier's status using `GET /classifiers/{classifier_id}`. In other words, use the classifier `GET` for a single classifier ID, rather than `GET /classifiers`, which gets all classifiers, and can trigger this issue. Note that `GET /classifiers/{classifier_id}` is also faster. You may also see this issue if you are repeatedly using `POST /classify` to classify new images while training is in progress; wait until training completes to classify new images using `POST /classify`.
