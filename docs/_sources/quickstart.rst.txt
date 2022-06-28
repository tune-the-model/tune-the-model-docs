Quickstart tutorial
============================

This guide will walk you through the basics of using the Model One Python SDK for solving text generation and classification problems. We have fine-tuned models to show you some possible applications, such as wine description generation, financial sentiment, cyber-bullying detection and review sentiment.

You can find the example containing the code below in the form of `a colab notebook <https://colab.research.google.com/github/beyondml/model-one-py/blob/main/playbook.ipynb>`_.

Install package
---------------
``pip install --upgrade model-one``

Set up public key
-----------------

.. code:: python

  import model_one


  model_one.set_api_key('eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyZWFkb25seSI6MSwidXNlcl9pZCI6InBsYXlib29rIn0.no2mYwFZv3q7JrARu8n3n5aAl1EJ3bPtFo7KgK32M6E')

Take a look at pretrained models
--------------------------------

.. code:: python

  print(model_one.ModelOne.models())

  GENERATOR_TASKS = {
      "winemag": "f9cab2f96d9e65a125264702489cad7a",
  }

  CLASSIFIER_TASKS = {
      "amazon_polarity": "13419a9f17bf52cc48f009a512a99735",
      "cyberbullying_tweets": "9323f9dbc976ea5dc6c8272eb90742f9",
      "financial_sentiment": "1ec02ac96b3e3cd7762bf1e6e2955eb3",
  }

Result:

.. code:: text

  [{'id': '0e19c4acc05f968c33cd7f3a9c8b337b', 'status': 'Ready', 'model_type': 'classifier', 'user_name': None}, {'id': '13419a9f17bf52cc48f009a512a99735', 'status': 'Ready', 'model_type': 'classifier', 'user_name': 'amazon_polarity'}, {'id': '1ec02ac96b3e3cd7762bf1e6e2955eb3', 'status': 'Ready', 'model_type': 'classifier', 'user_name': 'financial_sentiment'}, {'id': '232403e72187d646b1de68d7f9aca371', 'status': 'Ready', 'model_type': 'classifier', 'user_name': None}, {'id': '8b6a96a9a6eb5df4a783f7deab495cf1', 'status': 'Ready', 'model_type': 'classifier', 'user_name': None}, {'id': '9323f9dbc976ea5dc6c8272eb90742f9', 'status': 'Ready', 'model_type': 'classifier', 'user_name': 'cyberbullying_tweets'}, {'id': 'f9cab2f96d9e65a125264702489cad7a', 'status': 'Ready', 'model_type': 'generator', 'user_name': 'winemag-data'}]


Generate wine description by names
----------------------------------

.. code:: python

  winemag = model_one.ModelOne.from_id(GENERATOR_TASKS["winemag"])
  print(winemag.generate('Italy, Valpolicella classico 2013'))

Result:

.. code:: text

  Made with ripe cherry, prune and blueberry fruit, this wine is soft and creamy with a touch of sweetness. It's a rich and rich wine with a velvety texture and a long, slightly bitter finish.

Detect cyber bullying
---------------------

.. code:: python

  cyberbullying_tweets = model_one.ModelOne.from_id(CLASSIFIER_TASKS["cyberbullying_tweets"])
  print(cyberbullying_tweets.classify("take that Kat &amp; Andre, scum of the earth LOL #mkr. I just can't with them... #mykitchenrules"))

Result:

.. code:: text

  [0.360595703]

Financial sentiment analysis
----------------------------

.. code:: python

  financial_sentiment = model_one.ModelOne.from_id(CLASSIFIER_TASKS["financial_sentiment"])
  for s in (
      "Royal Dutch Shell to Buy BG Group for Nearly $70 Billion",
      "France raises concerns over proposed LSE-Deutsche Boerse deal",
      "Pertti Ervi is independent from the Company and its major shareholders",
  ):
      print("Result for \"%s\": %s" % (s, financial_sentiment.classify(s)))

Result:

.. code:: text

  Result for "Royal Dutch Shell to Buy BG Group for Nearly $70 Billion": [0.831054688, 0.0625, 0.106445312]
  Result for "France raises concerns over proposed LSE-Deutsche Boerse deal": [0.0148239136, 0.934082031, 0.0511169434]
  Result for "Pertti Ervi is independent from the Company and its major shareholders": [0.0143356323, 0.0256347656, 0.959960938]
  
Complete example
----------------

.. code:: python

  import model_one


  model_one.set_api_key('eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyZWFkb25seSI6MSwidXNlcl9pZCI6InBsYXlib29rIn0.no2mYwFZv3q7JrARu8n3n5aAl1EJ3bPtFo7KgK32M6E')


  print(model_one.ModelOne.models())

  GENERATOR_TASKS = {
      "winemag": "f9cab2f96d9e65a125264702489cad7a",
  }

  CLASSIFIER_TASKS = {
      "amazon_polarity": "13419a9f17bf52cc48f009a512a99735",
      "cyberbullying_tweets": "9323f9dbc976ea5dc6c8272eb90742f9",
      "financial_sentiment": "1ec02ac96b3e3cd7762bf1e6e2955eb3",
  }


  winemag = model_one.ModelOne.from_id(GENERATOR_TASKS["winemag"])
  print(winemag.generate('Italy, Valpolicella classico 2013'))

  cyberbullying_tweets = model_one.ModelOne.from_id(CLASSIFIER_TASKS["cyberbullying_tweets"])
  print(cyberbullying_tweets.classify("take that Kat &amp; Andre, scum of the earth LOL #mkr. I just can't with them... #mykitchenrules"))

  financial_sentiment = model_one.ModelOne.from_id(CLASSIFIER_TASKS["financial_sentiment"])
  for s in (
      "Royal Dutch Shell to Buy BG Group for Nearly $70 Billion",
      "France raises concerns over proposed LSE-Deutsche Boerse deal",
      "Pertti Ervi is independent from the Company and its major shareholders",
  ):
      print("Result for \"%s\": %s" % (s, financial_sentiment.classify(s)))

Next steps
----------

To learn more about finetuning our model with your data for different tasks read the following guides:

* :doc:`Classification <classifier/>`.
* :doc:`Generation <generator/>`.