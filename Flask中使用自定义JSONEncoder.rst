例如::

    return jsonify(now=datetime.now())

返回::

    {
        "now": "Fri, 16 Mar 2018 18:25:24 GMT"
    }

Flask本身是使用的一个自己实现的JSONEncoder, flask.json.JSONEncoder_.

自定义的实现参考：`Custom Flask JSONEncoder`_.

.. _Custom Flask JSONEncoder: http://flask.pocoo.org/snippets/119/



结合Django的一个CustomJSONEncoder的实现::

    class DjangoJSONEncoder(json.JSONEncoder):
        """
        JSONEncoder subclass that knows how to encode date/time, decimal types, and
        UUIDs.
        """
        def default(self, o):
            # See "Date Time String Format" in the ECMA-262 specification.
            if isinstance(o, datetime.datetime):
                r = o.isoformat()
                if o.microsecond:
                    r = r[:23] + r[26:]
                if r.endswith('+00:00'):
                    r = r[:-6] + 'Z'
                return r
            elif isinstance(o, datetime.date):
                return o.isoformat()
            elif isinstance(o, datetime.time):
                if is_aware(o):
                    raise ValueError("JSON can't represent timezone-aware times.")
                r = o.isoformat()
                if o.microsecond:
                    r = r[:12]
                return r
            elif isinstance(o, datetime.timedelta):
                return duration_iso_string(o)
            elif isinstance(o, (decimal.Decimal, uuid.UUID, Promise)):
                return str(o)
            else:
                return super().default(o)


结合两者，实现代码如下::



.. _flask.json.JSONEncoder: http://flask.pocoo.org/docs/0.12/api/#flask.json.JSONEncoder
