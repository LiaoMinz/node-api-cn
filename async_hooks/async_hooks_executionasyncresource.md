
<!-- YAML
added: v13.9.0
-->

* Returns: {Object} The resource representing the current execution.
  Useful to store data within the resource.

Resource objects returned by `executionAsyncResource()` are most often internal
Node.js handle objects with undocumented APIs. Using any functions or properties
on the object is likely to crash your application and should be avoided.

Using `executionAsyncResource()` in the top-level execution context will
return an empty object as there is no handle or request object to use,
but having an object representing the top-level can be helpful.

```js
const { open } = require('fs');
const { executionAsyncId, executionAsyncResource } = require('async_hooks');

console.log(executionAsyncId(), executionAsyncResource());  // 1 {}
open(__filename, 'r', (err, fd) => {
  console.log(executionAsyncId(), executionAsyncResource());  // 7 FSReqWrap
});
```

This can be used to implement continuation local storage without the
use of a tracking `Map` to store the metadata:

```js
const { createServer } = require('http');
const {
  executionAsyncId,
  executionAsyncResource,
  createHook
} = require('async_hooks');
const sym = Symbol('state'); // Private symbol to avoid pollution

createHook({
  init(asyncId, type, triggerAsyncId, resource) {
    const cr = executionAsyncResource();
    if (cr) {
      resource[sym] = cr[sym];
    }
  }
}).enable();

const server = createServer(function(req, res) {
  executionAsyncResource()[sym] = { state: req.url };
  setTimeout(function() {
    res.end(JSON.stringify(executionAsyncResource()[sym]));
  }, 100);
}).listen(3000);
```

