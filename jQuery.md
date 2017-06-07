#jQuery


## General

All code goes within <script> </script>
Document ready function
  $(document).ready(function() {});
Selection
  By element: $("element")
  By class: $(".class")
  By ID: $("#ID")
  Modify entire document: $("body")

## Functions

Class
  Add class: .addClass("class")
  Remove class: .removeClass("class")
CSS
  Change CSS: .css("property", "value");
Element
  Change properties: .prop("property", boolean)
  Remove element: .remove()
  Move element: .appendTo("destination")
  Clone element: .clone()
  Select parent of element: .parent()
  Select child of element: .children()
  Select nth child: $(".target:nth-child(n)")
  Select even/odd elements :  $(".target:even/odd")
Text
  Add HTML tags: .html("<>text</>")
  Alter text: .text("text")
