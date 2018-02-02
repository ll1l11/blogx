.. code-block:: python

    from fabric.api import prefix


    with prefix('~/.virtualenvs/py3/bin/activate'):
      run('pip install -r requirements.txt')
