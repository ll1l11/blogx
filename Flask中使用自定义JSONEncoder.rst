例如::

    return jsonify(now=datetime.now())

返回::

    {
        "now": "Fri, 16 Mar 2018 18:25:24 GMT"
    }

Flask本身是使用的一个自己实现的JSONEncoder, flask.json.JSONEncoder_.

一个实现实现参考：`Custom Flask JSONEncoder`_.

实现代码如下::

    from datetime import datetime, date, time
    import json
    import uuid
    import decimal

    from flask import Flask, jsonify


    class CustomJSONEncoder(json.JSONEncoder):
        def default(self, o):
            # See "Date Time String Format" in the ECMA-262 specification.
            if isinstance(o, datetime):
                return o.isoformat(sep=' ', timespec='seconds')
            if isinstance(o, date):
                return o.isoformat()
            if isinstance(o, time):
                return o.isoformat(timespec='seconds')
            if isinstance(o, (decimal.Decimal, uuid.UUID)):
                return str(o)
            else:
                return super().default(o)


    app = Flask(__name__)
    app.json_encoder = CustomJSONEncoder


    @app.route('/')
    def index():
        return jsonify(now=datetime.now())


    if __name__ == '__main__':
        app.run()


.. _flask.json.JSONEncoder: http://flask.pocoo.org/docs/0.12/api/#flask.json.JSONEncoder
.. _Custom Flask JSONEncoder: http://flask.pocoo.org/snippets/119/
