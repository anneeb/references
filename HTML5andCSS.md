# HTML5 and CSS

## Elements

Comment: <!-- ... -->
Head
  Style: <style> </style>
    By element: element {}
    By Class: .class {}
    By id: #id {}
Block-level
  Always starts on a new line and takes up the full width available
  Division: <div> </div>
  Headings: <h#>text</h#> where # = 1 - 6
  Paragraph: <p>text</p>
  Form: <form action="url" method="method"></form>
    Method: post (up to server)
    Label: <label for="thing">Label</label>
    Input: <input type="type" name="name" placeholder="placeholder" (required)>    
      Type: text, email, tel, submit (value="text")
    Text area: <textarea name="name" rows="num"></textarea>
Inline
  Does not start on a new line and only takes up as much width as necessary
  Span: <span> things </span>
  Image: <img src="url" alt="descriptor">
  Anchor: <a href="url">text</a>
  Dead links: href=#
Lists
  Unordered (bulleted): <ul> <li> </li> </ul>
  Ordered (numbered): <ol> <li> </li> </ol>
Inputs
  Text field: <input type="text">
    Required: cannot submit unless filled
    Placeholder: placeholder="text"
Buttons
  Submit: <button type="submit">submit</button>
  Radio: <label><input type="radio" name="text">text</label>
    Default checked: checked
  Checkbox: <label><input type="checkbox" name="text"> text</label>
    Default checked: checked

## Text tags and things

Italics: <em> </em>
Add real spaces: &nbsp;

## Attributes

Style: style="style-1: style-1; style-2: style-2;"
Class: class="class-1 class-2"
ID: id="id-1 id-2"

## Style

Style hierarchy
  element < class < ID < inline < !important
Text
  color: color;
  color: #000000; (RRGGBB, 0-9-A-F)
  color: #000; (RGB, 0-9-A-F)
  color: rgb(0, 0, 0); (RGB, 0-255)
Fonts
  font-size: #px
  font-family: firstchoice, default; (serif, sans-serif)
Size
  width: #px;
  height: #px;
Borders
  border-color: color; (red, green, blue, etc)
  border-width: #px;
  border-style: style; (solid, dashed, etc)
  border-radius: #px or #%;
Background
  background-color: color;
Padding: space between element and border
  padding: #px #px #px #px; (top right bottom left)
  padding-top/right/bottom/left: #px
Margin: space between border and surrounding elements
  margin: #px #px #px #px; (top right bottom left)
  margin-top/right/bottom/left: #px
