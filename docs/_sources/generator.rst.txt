Generator
=========

Learn how to fine-tune a model that can generate text.

Install package
---------------
``pip install --upgrade model-one``

Set up the key
--------------

In case you don't have a key yet, please follow :doc:`this guide <api_key/>`.

.. code:: python

  import model_one


  model_one.set_api_key(os.environ.get("MODEL_ONE_KEY"))

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

A training phase typically takes a couple of hours, but for a small dataset it will be finished in around 30 minutes.

Calling just one method will under the hood do the following for you: create a model, save it to the file, upload datasets and put the model in the queue for training.

.. code:: python

  model = model_one.train_generator(
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

  import model_one
  import pandas as pd

  model_one.set_api_key('YOUR_API_KEY')

  tdf = pd.read_csv('train.csv')
  vdf = pd.read_csv('test.csv')

  model = model_one.train_generator(
      'filename.json',
      tdf['inputs'], tdf['outputs'],
      vdf['inputs'], vdf['outputs']
  )

  model.wait_for_training_finish()

  the_answer = model.generate('The Answer to the Ultimate Question of Life, the Universe, and Everything')
  print(the_answer)