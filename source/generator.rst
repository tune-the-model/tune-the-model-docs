Generator
=========

Learn how to fine-tune a model that can generate text.

Install package
---------------
``pip install --upgrade tune-the-model``

Set up the key to environment variable
--------------------------------------

In case you don't have a key yet, please follow :doc:`this guide <api_key/>`.

.. code:: bash

  export TTM_API_KEY=<insert your API key here>

Load the dataset
--------------------------------------

The dataset consists of lines with the following fields:

Example:

.. code::

  question,answer

Let's load the dataset:

.. code:: python

  import pandas as pd


  tdf = pd.read_csv('train.csv')
  vdf = pd.read_csv('test.csv')


Fine tune a model
----------------------------------

A training phase takes between 30 minutes and 5 hours depending on a dataset size.

Calling just one method will under the hood do the following for you: create a model, save it to the file, upload datasets and put the model in the queue for training.

.. code:: python

  model = ttm.train_generator(
      'generator.json',
      tdf['inputs'], tdf['outputs'],
      vdf['inputs'], vdf['outputs']
  )

  model.wait_for_training_finish()

Infer
-----

.. code:: python

  the_answer = model.generate('The Answer to the Ultimate Question of Life, the Universe, and Everything')
  print(the_answer)

Complete example
----------------

.. code:: python

  import tune_the_model as ttm
  import pandas as pd

  tdf = pd.read_csv('train.csv')
  vdf = pd.read_csv('test.csv')

  model = ttm.tune_generator(
      'filename.json',
      tdf['inputs'], tdf['outputs'],
      vdf['inputs'], vdf['outputs']
  )

  model.wait_for_training_finish()

  the_answer = model.generate('The Answer to the Ultimate Question of Life, the Universe, and Everything')
  print(the_answer)
