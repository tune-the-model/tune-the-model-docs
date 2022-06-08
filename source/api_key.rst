Getting your API Key
====================

The Model One API uses API keys for authentication. Visit `Model One's landing page <https://model-one.ai>`_ to obtain the API key you'll use in your requests.

Your API key is a secret. Please, do not share it with others.

Request an API Key
------------------
 
As we are in closed beta stage, we manually review and process all new applications.

In order to obtain API access, please fill out the registration form on `Model One's landing page <https://model-one.ai>`_.

Wait for a letter from us
-------------------------
 
We will try to contact you as quickly as possible. We might ask you to tell us a little bit about yourself and about how you plan to use the API, primarily for two important reasons:

- We want to be sure that our technology is used ethically
- We would like to make you familiar with our current limitations (there are some) if they potentially affect your use-case

Once we get to know each other, we'll send you your API key. Welcome to Model One!

Test your API key
-----------------

- Using curl:

  .. code:: bash
  
    $ curl --url "https://api.todo.ml/v0/models" --header "Authorization: <insert your API key here>"

  .. code::

    {"models": []}

- Using Python:

  .. code:: python

     import requests
     requests.get('https://api.todo.ml/v0/models', headers={'Authorization': '<insert your API key here>'}).json()

  .. code:: 

      {'models': []}

If you run into any problems, please write to `support@todo.ml <mailto:support@todo.ml>`_

Add your API key to ~/.bashrc
-----------------------------

  *OS: Linux or macOS*

  On Linux, run the following command; it will add the instructions to set the environment variable ``MODEL_ONE_KEY`` to your ``~/.bashrc``.

  .. code:: bash
  
      echo 'export MODEL_ONE_KEY=<insert your API key here>' >>~/.bashrc

  On macOS, use ``.bash_profile`` instead of ``.bashrc``:

  .. code:: bash
  
      echo 'export MODEL_ONE_KEY=<insert your API key here>' >>~/.bash_profile