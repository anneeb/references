# Javascript: Extended

## XML Http Request (XHR)

Get
  Define: get() {}
  1. Create a request constant
    const req = new XMLHttpRequest()
  2. Add event listener to the request
    req.addEventListener("load", show)
  3. Initialize the request
    req.open("GET", 'url')
  4. Send the request
    req.send
Show
  Define: show(event, data) {}
  1. Parse the response
    var resp = JSON.parse(this.responseText)
  2. Build HTML
    const html = `<ul>${resp.map(r => '<li>' + r.name + '</li>').join('')}</ul>`
  3. Insert HTML
    target.innerHTML = html
Handlebars
  Define: <script id="response-template" type="text/x-handlebars-template"></script>
  Arguments: {{name of property of the context object}}
  Each helper: {{#each}} {{/each}}
Show with handlebars
  1. Parse the response
    const resp = JSON.parse(this.responseText)
  2. Get the handlebars script
    const src = document.getElementById("response-template").innerHTML
  3. Compile the handlebars script
    const template = Handlebars.compile(src)
  4. Build HTML
    const html = template(resp)
  5. Insert HTML
    target.innerHTML = html

## Asynchronous JavaScript and XML (AJAX)

Set up
  Library: <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
  Document ready: $(document).ready(function(){})
Get
  Define: $.get("source", function(data){})
  Fail: .fail(function(error){})
  Done: .done(function(data) {}
Ajax
  $.ajax(
    {url: url,
    contentType: 'application/json',
    dataType: 'jsonp',
    success: callback
  })

## Fetch

Define: fetch(url, {body})
Parse JSON: .then(res => res.json())

## Modular Coding

Named
  Export: export default { key: value, key: value }
  Import: import newName from 'relative path'
  Import: import { key } from 'relative path'
Default
  Export: export default Object
  Import: import Object from 'relative path'

## Babel

In .babelrc,
  { "presets": ["es2015", "react"],
    "plugins": ["plugin", "plugin"]  }
Plugins
  React: babel-preset-es2015, babel-preset-react
  ES2015 destructing: transform-es2015-destructuring
  Object rest and spread: babel-plugin-transform-object-rest-spread
  Class properties: babel-plugin-transform-class-properties
