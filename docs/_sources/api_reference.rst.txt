API Reference
=============

Introduction
------------

You can interact with the API through HTTP requests from any language or via our official Python SDK.

To install the Python SDK, run the following command:

``pip install --upgrade model-one``

Authentication
--------------

The Model One API uses API keys for authentication. Follow :doc:`this guide <api_key/>` to obtain the API key you'll use in your requests. Your API key is a secret. Please, do not share it with others.

Models
------

List, create, delete and describe the fine-tuned models.

List models
^^^^^^^^^^^

Lists the available fine-tuned models, and provides basic information about each one such as the owner and availability.

Curl:

.. code:: bash

  curl "https://api.todo.ml/v0/models" \
    -H "Authorization: <insert your API key here>"

Python:

.. code:: python

  import model_one


  model_one.set_api_key(os.environ.get("MODEL_ONE_KEY"))
  print(model_one.ModelOne.models())

Create model
^^^^^^^^^^^^

Creates a new model.

.. code:: bash

  curl -X 'POST' \
    'https://api.beyond.ml/v0/models' \
    -H 'accept: application/json' \
    -H 'Content-Type: application/json' \
    -d '{
      "model_type": "string",
      "model_params": {
        "train_iters": 0,
        "num_classes": 0
      },
      "name": "string"
    }'

Get model's status
^^^^^^^^^^^^^^^^^^

Fetches a model instance, providing information about the model such as .

Curl:

.. code:: bash

  curl "https://api.todo.ml/v0/models/<model_name>/status" \
    -H "Authorization: <insert your API key here>"

Delete model
^^^^^^^^^^^^

Training
--------

2. Upload datasets
3. Start training
4. Get model info, monitor progress
5. Cancel training


Inference
---------

1. Generate
2. Score
3. Classify