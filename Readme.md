
# Connect JSON-RPC

## Installation

    $ npm install connect-jsonrpc

## Examples

The _jsonrpc_ middleware provides JSON-RPC 2.0 support. Below is an example exposing the _add_ and _sub_ methods:

	  var math = {
	      add: function(a, b, fn){
	          fn(null, a + b);
	      },
	      sub: function(a, b, fn){
	          fn(null, a - b);
	      }
	  };
    
	  var date = {
	      time: function(fn){
	          fn(null, new Date().toUTCString());
	      }
	  };
    
	  connect.createServer(
	      require('connect-jsonrpc')(math, date)
	  );
    
When you wish to pass an exception simply invoke `fn(err)`, or pass the error code `fn(jsonrpc.INVALID_PARAMS)`. Otherwise `fn(null, result)` will respond with the given results.

## Example Requests

Regular params:

    $ curl -H "Content-Type: application/json" -d '{ "jsonrpc": "2.0", "method": "add", "params": [1,2], "id":2 }' http://localhost:3000

Named params:

    $ curl -H "Content-Type: application/json" -d '{ "jsonrpc": "2.0", "method": "add", "params": { "b": 1, "a": 2 }, "id":2 }' http://localhost:3000



































































































