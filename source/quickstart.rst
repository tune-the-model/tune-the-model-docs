Quickstart tutorial
============================

This guide will walk you through the basics of using the Model One Python SDK for solving text generation and classification problems. We have fine-tuned models to show you some possible applications, such as wine description generation, financial sentiment, cyber-bullying detection and review sentiment.

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


Generate wine description by names
----------------------------------

.. code:: python

  winemag = model_one.ModelOne.from_id(GENERATOR_TASKS["winemag"])
  print(winemag.generate('Italy, Valpolicella classico 2013'))


Detect cyber bullying
---------------------

.. code:: python

  cyberbullying_tweets = model_one.ModelOne.from_id(CLASSIFIER_TASKS["cyberbullying_tweets"])
  print(cyberbullying_tweets.classify("take that Kat &amp; Andre, scum of the earth LOL #mkr. I just can't with them... #mykitchenrules"))

Financial sentiment analysis
----------------------------

.. code:: python

  financial_sentiment = model_one.ModelOne.from_id(CLASSIFIER_TASKS["financial_sentiment"])
  print(financial_sentiment.classify("Royal Dutch Shell to Buy BG Group for Nearly $70 Billion"))
  print(financial_sentiment.classify("France raises concerns over proposed LSE-Deutsche Boerse deal"))
  print(financial_sentiment.classify("Pertti Ervi is independent from the Company and its major shareholders"))
  


Full example
------------

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
  print(financial_sentiment.classify("Royal Dutch Shell to Buy BG Group for Nearly $70 Billion"))
  print(financial_sentiment.classify("France raises concerns over proposed LSE-Deutsche Boerse deal"))
  print(financial_sentiment.classify("Pertti Ervi is independent from the Company and its major shareholders"))