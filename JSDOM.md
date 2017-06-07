# Javascript: DOM (document object model)

## The Tree

Window (God Object)
  Define: window
  Return entire document: window.document
  Return inner width of browser window: window.innerWidth
  Return inner height of browser window: window.innerHeight
Document (Object)
  Define: document
  Return all nodes inside document object: document.all
  Return type of content contained: document.contentType
  Return URL of document object: document.URL
Forms, anchors, and images (nodes)
  Add elements: appendChild
  Remove elements: removeChild

## Selecting Nodes

Selector
  Return an element: document.querySelector("element")
  Return all elements as an array: .querySelectorAll("element")
  Nth child: .querySelector("element:nth-child(n)")
Get elements
  Tag name: .getElementsByTagName
  ID: .getElementsById
  Class name: .getElementsByClassName
Inner values
  Value: .nodeValue
  HTML: .innerHTML
  Text: .innerText

## Creating, Inserting, and Deleting Nodes

Create an element: var element = document.createElement("tagname")
Adding HTML: element.innerHTML = "text"
Adding style: element.style.property = "value"
Append element to existing DOM node: target.appendChild(element)
Remove selected node: .remove()
