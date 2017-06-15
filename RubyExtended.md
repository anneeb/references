# Ruby: Extended

## Basics

REPL: read, evaluate, print, loop
Interactive Ruby
  Enter: irb
  Exit: exit
Pry
  Pauses code and enters a REPL and encapsulates the context of the current scope
  Set up: require 'pry'
  Enter: binding.pry
  Exit: exit

## Command Line Interface (CLI) Applications

File structure
  ├── bin/
  │     Code related to running actual program
  ├── config/
  │     Application's environment
  │     Includes source code, method definitions, classes, etc.
  │     Responsible for file requirements, establishing connections, file access
  ├── lib/ (app/)
  │     Defines what the program can do
  │     Includes all methods and classes the program needs
  ├── spec/ (test/)
  │     Tests
  ├── .rspec, .learn, gemfile, gemfile.lock, rakefile
  │     Tooling and support
Shebang line
  Tells the shell which interpreter to use to execute remainder of file
  Example: #!/usr/bin/env ruby
CHMOD
  Grant file execute permissions: $ chmod +x <file_name>
User input
  Yes or no: (Y/n)
    Will accept: yes, no, N, n, etc.
  Define input interface: a string with options
  Capture input: var = gets
    Remove any new lines: gets.chomp
    Remove any new lines or trailing whitespace: gets.strip  
  CLI will wait for user input and enter/return
Link to another file: require_relative

## APIs

OpenURI
  Parse URL: uri = URI.parse(URL)
  Get: response = Net::HTTP.get_response(uri)
  Parse: JSON.parse(response.body)
RestClient
  Gem: require 'rest-client'
  Get and parse: JSON.parse(RestClient.get('url'))

## Scraping

Document requirements: nokogiri, open-uri
Grab html: variable = open("url")
Convert html into NodeSet: Nokogiri::HTML(variable)
Save NodeSet in an operable variable: doc = Nokogiri::HTML(variable)
CSS selector: doc.css("style")
Attribute selector: .attribute("attr")
Select text within a block: .text

## Teh Interwebs

URLs / URIs
  Uniform Resource Locators / Identifiers
  Protocol: https, http, smpt, ftp
  Domain: x.com
  Resource: /path
HTTP verbs
  HEAD: Asks for a response like a GET but without the body
  GET: Retrieves a representation of a resource
  POST: Submits data to be processed in the body of the request
  PUT: Uploads a representation of a resource in the body of the request
  DELETE: Deletes a specific resource
  TRACE: Echoes back the received request
  OPTIONS: Returns the HTTP methods the server supports
  CONNECT: Converts the request to a TCP/IP tunnel (generally for SSL)
  PATCH: Apply a partial modification of a resource

## Rack

Basics
  Run code: rackup config.ru
  application.rb:
    class Application
      def call(env)
        resp = Rack::Response.new
        resp.finish
      end
    end
  config.ru:
    require_relative "./config/environment.rb"
    run Application.new
    use Rack::Reloader, 0 (auto restart server, middleware)
Rack calls
  Define: def call(env) <br> [status, header, body] <br> end
  Must return array with integer/string, hash, and ennumerable
    Status: three digit number
    Header: hash
    Body: enumerable
Rack::Response
  Makes status, header, body array for us
  Defaults status code to 200
Rack::Request
  Parse env to new request: req = Rack::Request.new(env)
  Filter paths: req.path.match(/path/)
Parameters
  GET parameters: ?
  Key-value pair: q=term
  Access value: = req.params["q"]
Rack commands
  Puts things to html: resp.write "string"
  Add line break after string: resp.write "string\n"
  Generate random number: Kernel.rand(range)
  Set status code: resp.status = number

## ERB - Embedded ruby

Basics
  Templating engine
  Display ruby tags: <%= ruby %>
  Background ruby tags: <% ruby %>
Set up
  Require gem: require 'erb'
  Create render method within class:
    def render(template)
      path = File.expand_path("../views/#{template}", __FILE__)
      ERB.new(File.read(path)).result(binding)
    end
Surrounding HTML
  In /views: layout.erb, <%= yield %> in body

## Capybara

Types of tests
  Unit: models and how they interact with databases
  Controller: delivering the appropriate data to a user
  Integration (end-to-end): entire application stack
Set up (spec/spec_helper)
  require 'rspec'
  require 'capybara/rspec'
  require 'capybara/dsl'
  RSpec.configure do |config|
    config.include Capybara::DSL
    config.order = 'default'
  end
  def app
    Rack::Builder.parse_file('config.ru').first
  end
  Capybara.app = app
Test actions
  Visit page: visit '/'
  Fill in: fill_in(:field, :with => "value")
  Click button: click_button "button"
Text expectations
  Def: expect(page).to method
  Have text: have_text("text")
  Have selector: have_selector("selector")
  Have field: .to have_field(:field)
