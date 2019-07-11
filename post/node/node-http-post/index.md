---
title: Make an HTTP POST request using Node
seotitle: How to make an HTTP POST request using Node
description: "Find out how to make an HTTP POST request using Node"
date: 2018-08-11T15:00:00+02:00
tags: node
tags_weight: 33
path: node-http-post
---

There are many ways to perform an HTTP POST request in Node, depending on the abstraction level you want to use.

The simplest way to perform an HTTP request using Node is to use the [Axios library](https://flaviocopes.com/axios/):

```js
const axios = require('axios')

axios.post('https://flaviocopes.com/todos', {
  todo: 'Buy the milk'
})
.then((res) => {
  console.log(`statusCode: ${res.statusCode}`)
  console.log(res)
})
.catch((error) => {
  console.error(error)
})
```

Another way is to use the [Request library](https://github.com/request/request):

```js
const request = require('request')

request.post('https://flaviocopes.com/todos', {
  json: {
    todo: 'Buy the milk'
  }
}, (error, res, body) => {
  if (error) {
    console.error(error)
    return
  }
  console.log(`statusCode: ${res.statusCode}`)
  console.log(body)
})
```

The 2 ways highlighted up to now require the use of a 3rd party library.

A POST request is possible just using the Node standard modules, although it's more verbose than the two preceding options:

```js
const https = require('https')

const data = JSON.stringify({
  todo: 'Buy the milk'
})

const options = {
  hostname: 'flaviocopes.com',
  port: 443,
  path: '/todos',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Content-Length': data.length
  }
}

const req = https.request(options, (res) => {
  console.log(`statusCode: ${res.statusCode}`)

  res.on('data', (d) => {
    process.stdout.write(d)
  })
})

req.on('error', (error) => {
  console.error(error)
})

req.write(data)
req.end()
```