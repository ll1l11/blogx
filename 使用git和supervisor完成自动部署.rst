在服务器创建git仓库::

    mkdir -p ~/git/demo.git
    cd ~/git/demo.git
    git init --bare

设置hooks, ~/git/demo.git/hooks/post-receive::

    #!/bin/sh
    TRAGET="$HOME/production/demo"
    GIT_DIR="$HOME/git/demo.git"
    BRANCH="master"

    while read oldrev newrev ref
    do
        # only checking out the master (or whatever branch you would like to deploy)
        if [[ $ref = refs/heads/$BRANCH ]];
        then
                echo "Ref $ref received. Deploying ${BRANCH} branch to production..."
                git --work-tree=$TRAGET --git-dir=$GIT_DIR checkout -f
        else
                echo "Ref $ref received. Doing nothing: only the ${BRANCH} branch may be deployed on this server."
        fi
    done

    exit 0

