自动部署最新的提交的代码

.. code-block:: sh

    git checkout $GIT_COMMIT
    # pipenv install --ignore-pipfile
    supervisorctl restart your-project
    pipenv install --ignore-pipfile
