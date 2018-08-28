使用git进行简单的自动部署
============================

在服务器上初始化远程仓库
------------------------

.. code-block:: sh

    git init hello.git


hooks
---------

.. code-block:: sh

    cd hello.git
    vim hooks/post-receive


内容如下::

    #!/bin/sh

    while read oldrev newrev ref
    do
        echo "******************** $oldrev $newrev $ref *****************************"
        echo "Commit ref received.  Deploying ..."
        git --work-tree=/home/ubuntu/hello/ --git-dir=/home/ubuntu/git/hello.git checkout -f $newrev
        sudo super
        echo "******************** $oldrev $newrev $ref *****************************"
    done


执行::

    chmod +x hooks/post-receive




