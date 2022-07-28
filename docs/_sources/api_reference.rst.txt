API Reference
=============

Introduction
------------

You can interact with the API through HTTP requests from any language or via our official Python SDK.

Authentication
--------------

The Tune the Model API uses API keys for authentication. Follow :doc:`this guide <api_key/>` to obtain the API key you'll use in your requests. Your API key is a secret. Please, do not share it with others.

Models
------

List, create, delete and describe the fine-tuned models.

List models
^^^^^^^^^^^

Lists the available fine-tuned models, and provides basic information about each one such as the owner and availability.

Request:

.. code:: bash

  curl "https://api.tunethemodel.com/v0/models" \
    -H "Authorization: <insert your API key here>"

Response:

.. code:: text

  {
   "models": [
    {
     "status": "Ready",
     "model_name": "9323f9dbc976ea5dc6c8272eb90742f9",
     "model_type": "classifier",
     "user_name": "cyberbullying_tweets",
     "last_updated_time": "2022-05-07 20:58:10.878585"
    },
    {
     "status": "Ready",
     "model_name": "f9cab2f96d9e65a125264702489cad7a",
     "model_type": "generator",
     "user_name": "winemag-data",
     "last_updated_time": "2022-05-06 17:15:59.202724"
    }
   ]
  }

Create a model
^^^^^^^^^^^^^^

.. option:: model_type <model type>

   Model type can be either generator or classifier.

.. option:: name <name>

   Name of a model.

.. option:: model_params.num_classes <number of classes>

   Creates a model for a multiclass classification task with <number of classes> classes.

Request:

.. code:: bash

  curl -X 'POST' \
    'https://api.tunethemodel.com/v0/models' \
    -H "Authorization: <insert your API key here>" \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -d '{
      "model_type": "classifier",
      "model_params": {
        "num_classes": 3
      },
      "name": "my-shiny-classifier"
    }'

Response:

.. code:: text

 {
  "status": "Created",
  "model_name": "c4319ce72c6c48dfa0754faf3d083f02",
  "model_type": "classifier",
  "model_params": {
   "num_classes": 3
  },
  "user_name": "my-shiny-classifier",
  "last_updated_time": "2022-06-10 17:52:35.81619"
 }

Get model's status
^^^^^^^^^^^^^^^^^^

Fetches a model instance, providing information about the model such as .

.. option:: model_name <model name>

   Id obtained from model_name field on previous step.

Request:

.. code:: bash

  curl "https://api.tunethemodel.com/v0/models/<model_name>/status" \
    -H "Authorization: <insert your API key here>"

Response:

.. code:: text

 {
  "status": "Created",
  "model_name": "c4319ce72c6c48dfa0754faf3d083f02",
  "model_type": "classifier",
  "model_params": {
   "num_classes": 3
  },
  "user_name": "my-shiny-classifier",
  "last_updated_time": "2022-06-10 17:52:35.81619"
 }

Delete a model
^^^^^^^^^^^^^^

Request:

.. code:: bash

  curl "https://api.tunethemodel.com/v0/models/<model_name>/delete" \
    -H "Authorization: <insert your API key here>" \
    -X DELETE

Response:

.. code:: text

 {
  "status": "Created",
  "model_name": "c4319ce72c6c48dfa0754faf3d083f02",
  "model_type": "classifier",
  "model_params": {
   "num_classes": 3
  },
  "user_name": "my-shiny-classifier",
  "last_updated_time": "2022-06-10 17:59:41.523746"
 }