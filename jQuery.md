#jQuery

## General

All code goes within <script> </script>
Selectors
  By element: $("element")
  By class: $(".class")
  By ID: $("#ID")
  Modify entire body: $("body")  

## Element methods

Adding
  Class: .addClass("class")
  HTML tags: .html("<>text</>")
  Text to HTML tag: .append("text")
  Anchor or move element: .appendTo("destination")
Removing
  Element: .remove()
  Class: .removeClass("class")
Modifying
  Properties: .prop("property", boolean)
  CSS: .css("property", "value")
  Text: .text("text")
Selecting
  Parent: .parent()
  Child: .children()
  Value: .val()
  Nth child: $(".target:nth-child(n)")
  Even/odd elements :  $(".target:even/odd")

##

Document ready: $(document).ready(function() {})
Events handler: $("selector").on("eventname", function(){ //action })
Prevent default: in events handler, function(event){ event.preventDefault()}
Stop propagation: event.stopPropagation();
