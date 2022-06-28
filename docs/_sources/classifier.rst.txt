Classifier
==========

Learn how to fine-tune a model that can classify where a tweet contains irony or not.

Install package
---------------
``pip install --upgrade model-one``

Set up the key to environment variable
--------------------------------------

In case you don't have a key yet, please follow :doc:`this guide <api_key/>`.

.. code:: bash

  export MODEL_ONE_API_KEY=<insert your API key here>

Load TweetEval irony detection dataset
--------------------------------------

The dataset consists of lines with the following fields:

* text: a string feature containing the tweet.
* label: an int classification label with the following mapping:

  * 0: non_irony
  * 1: irony

The text in the dataset is in English, as spoken by Twitter users.  

Example:

.. code::

  {'label': 1, 'text': 'seeing ppl walking w/ crutches makes me really excited for the next 3 weeks of my life'}

Let's load the dataset:

.. code:: python

  from datasets import load_dataset
  import pandas as pd


  dataset = load_dataset("tweet_eval", "irony")
  train = pd.DataFrame(dataset["train"])
  validation = pd.DataFrame(dataset["validation"])


Fine tune a model
----------------------------------

A training phase takes between 30 minutes and 5 hours depending on a dataset size.

.. code:: python

  model = model_one.train_classifier(
      "model-one-tweet_eval-irony.json",
      train["text"], 
      train["label"], 
      validation["text"], 
      validation["label"]
  )
  classifier.wait_for_training_finish()


Infer
-----

.. code:: python

  res_validation = [model.classify(input=text) for text in dataset["validation"]["text"]]

  res = [model.classify(input=text) for text in dataset["test"]["text"]]


Find the best threshold
-----------------------

.. code:: python

  from sklearn.metrics import precision_recall_curve
  from sklearn.metrics import classification_report
  import numpy as np
  
  precision, recall, thresholds = precision_recall_curve(dataset["validation"]["label"], res_validation)

  f1_scores = 2 * recall * precision / (recall + precision)
  print("Best threshold: ", threshold)
  print("Best F1-Score: ", np.max(f1_scores))



Complete example
----------------

.. code:: python

  from datasets import load_dataset
  from sklearn.metrics import classification_report
  from sklearn.metrics import precision_recall_curve
  import pandas as pd
  import numpy as np

  import model_one


  dataset = load_dataset("tweet_eval", "irony")
  train = pd.DataFrame(dataset["train"])
  validation = pd.DataFrame(dataset["validation"])

  model = model_one.train_classifier(
      "model-one-tweet_eval-irony.json",
      train["text"],
      train["label"],
      validation["text"],
      validation["label"],
  )

  model.wait_for_training_finish()
  res_validation = [model.classify(input=text) for text in dataset["validation"]["text"]]
  precision, recall, thresholds = precision_recall_curve(dataset["validation"]["label"], res_validation)

  res = [model.classify(input=text) for text in dataset["test"]["text"]]

  f1_scores = 2 * recall * precision / (recall + precision)
  threshold = thresholds[np.argmax(f1_scores)]
  print("Best threshold: ", threshold)
  print("Best F1-Score: ", np.max(f1_scores))
