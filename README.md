kuji
====

###Asynchronous Control Flow library for Node.

Browsers are not supported yet, it will be added later.

##Control Flow
`kuji.inline` runs tasks **in-line**:

``` javascript
var kuji = require('kuji');

kuji.inline([
  function (next) {
    next();
  },
  function (next) {
    next();
  },
  function (next) {
    next();
  },
  function (next) {
    next();
  }
]);

```
`kuji.parallel` runs tasks **in parallel** and goes to the final callback when all tasks finished:

``` javascript
var kuji = require('kuji');

kuji.parallel([
  function (next) {
    next();
  },
  function (next) {
    next();
  },
  function (next) {
    next();
  },
  function (next) {
    next();
  }
], function () {
  // This will be executed when all will be finished
});

```
`kuji.graph` permits you to easily run __tasks graphs__:

``` javascript
var kuji = require('kuji'),
    dependsOn = kuji._dependsOn;

kuji.graph({
  a: function (next) {
    next()
  },
  b: function (next) {
    next();
  },
  c: function (next) {  
    next();
  },
  d: dependsOn('a', function (next) {
    next();
  }),
  e: dependsOn(['d', 'c'], function () {

  })
}, function () {
  // This will be executed at the end of your graph
});

```

##Coming next
- Error handling through next()
- Passing values through next()
- Benchmark
- Perfomance optimization

##Testing
To run the tests :
```
mocha
```

##License
MIT
