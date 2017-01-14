# Micro API

### Summary

Minimal routing layer for building JSON APIs with Zeit's [Micro](https://github.com/zeit/micro)

[![CircleCI](https://circleci.com/gh/possibilities/micro-api.svg?style=svg)](https://circleci.com/gh/possibilities/micro-api)

### Installation

```javascript
npm install micro micro-api
```

### Usage

```javascript
// index.js
const microApi = require('./index')
const handlers = require('./handlers')

const api = microApi([
  {
    method: 'post',
    path: '/foos',
    handler: handlers.createFoo,
  },
  {
    method: 'get',
    path: '/foos/:fooId',
    handler: handlers.showFoo,
  },
])

module.exports = api
```

```javascript
// handlers.js
const uuid = require('uuid')

// In memory database
const foos = []

const createFoo = foo => {
  // Build up the new item
  const newFoo = Object.assign({}, foo, { id: uuid() })
  // Add it to the database
  foos.push(newFoo)
  return newFoo
}

// Find and return by id
const showFoo = (body, { fooId }) => foos.find(f => f.id === fooId)

module.exports = { createFoo, showFoo }
```

### Run

```
micro -p 3000 ./index.js
```

See [micro](https://github.com/zeit/micro#documentation) documentation for complete usage.
