# RESTify

## Server

Create server
  Define: restify.createServer()

## Handlers

Define
  function (req, res, next) { ...next() } or array of functions
Pre routing
  Define: server.pre(handler)
  It: runs for all routes before routing occurs
Post routing
  Define: server.use(handler)
  It: only runs after finding a matching route
  Common handlers
    Accept parser: restify.plugins.acceptParser(server.acceptable)
    Query parser: restify.plugins.queryParser
    Body parser: restify.plugins.bodyParser
    Set headers: within function, res.setHeaders('key', 'value')

## Routes

Methods
  Define: server.verb(opts, handler)
    Get: get (retrieves a representation of a resource)
    Post: post (submits data to be processed in the body of the request)
    Put: put (uploads a representation of a resource in the body of the request)
    Patch: patch (apply a partial modification of a resource)
    Delete: del (deletes a specific resource)
    Head: head (asks for a response like a GET but without the body)
    Options: opt (returns the HTTP methods the server supports)
Options
  Define: string or regex or object
  Static route: '/path'
  Parameterized route: '/path/:param'
  Object: {
    name: string,
    path: string or regex,
    version: string or array of strings
  }
Handler
  Includes: res.send() or res.json()

## Node Wrappers

Listen
  Define: server.listen('port', callback)
