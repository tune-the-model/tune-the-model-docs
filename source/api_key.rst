Getting your API Key
====================

The Tune the Model API uses API keys for authentication. Visit `Tune the Model's landing page <https://tunethemodel.com>`_ to obtain the API key you'll use in your requests.

Your API key is a secret. Please, do not share it with others.


Test your API key using curl
----------------------------

.. code:: bash

  $ curl --url "https://api.tunethemodel.com/v0/models" --header "Authorization: <insert your API key here>"

.. code::

  {"models": []}

If you encounter any problems, please write to `support@tunethemodel.com <mailto:support@tunethemodel.com>`_.

Set up the key to environment variable
--------------------------------------

.. code:: bash

  export TTM_API_KEY=<insert your API key here>

Add your API key to ~/.bashrc
-----------------------------

  *OS: Linux or macOS*

  On Linux, run the following command; it will add the instructions to set the environment variable ``TTM_API_KEY`` to your ``~/.bashrc``.

  .. code:: bash

      echo 'export TTM_API_KEY=<insert your API key here>' >> ~/.bashrc

  On macOS, use ``.bash_profile`` instead of ``.bashrc``:

  .. code:: bash

      echo 'export TTM_API_KEY=<insert your API key here>' >> ~/.bash_profile
