例如::

    return jsonify(now=datetime.now())

返回::

    {
        "now": "Fri, 16 Mar 2018 18:25:24 GMT"
    }


自定义的实现参考：`Custom Flask JSONEncoder`_.


.. _Custom Flask JSONEncoder: http://flask.pocoo.org/snippets/119/
