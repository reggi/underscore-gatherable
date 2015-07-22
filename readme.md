# Underscore Gatherable

Allow for any object of functions to be gatherable.

```bash
npm install underscore-gatherable
```

## Example

```javascript
var _ = require("underscore")
_.mixin(require("underscore-gatherable"))

var middleware = _.makeGatherable()

middleware.next = function(){
  return function(req, res, next){
    return next()
  }
}

middleware.json = function(){
  return function(req, res, next){
    return res.json({"name": "tobi"})
  }
}

_.extendGatherable(middleware)

var use = [
  middleware.next(),
  middleware.json()
]

console.log(use) // [ [function], [function] ]

//or

var use = middleware
  .gather()
  .next()
  .json()
  .value()

console.log(use)  // [ [function], [function] ]
```
