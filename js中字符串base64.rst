.. code-block:: javascript

    let username = 'username'
    let password = '123456'
    const hash = new Buffer(`${username}:${password}`).toString('base64')
    console.log('###', hash)
