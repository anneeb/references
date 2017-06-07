# Sinatra

## General
Basics
  Run code: rackup app.rb
  app.rb: class App < Sinatra::Base <br> body <br> end
  config.ru: require 'sinatra' <br> require_relative './app.rb' <br> run App
Shotgun
  Starts Rack with automatic code reloading
  Run code: shotgun filename.ex
  Use specific port: shotgun filename.ex -p xxxx (3000+)
  Default file to run: config.ru
MVC
  Models: where data is manipulated and/or saved
    Ruby classes, databases
  Views: front end, interacts with user directly, consist of HTML, CSS and JS
    .erb files with HTML and embedded Ruby
  Controllers: go-between for models and views
    "Routes" that take request from browser (GET, POST), run code based on those requests using models, render the erb view files

## File Structure

├── Gemfile (holds all gems need for application)
├── README.md
├── app (hold MVC directories)
│   ├── controllers (application configurations, routes, and controller actions)
│   │   └── application_controller.rb
│   │         ApplicationController class that inherits from Sinatra::Base
│   │         Configure block to tell the controller where to look to find the views
│   │         GET request that loads the index.erb file
│   ├── models (data and object logic)
│   │   └── model.rb (table in database)
│   └── views (what the user sees)
│       └── index.erb
├── config
│   └── environment.rb
│         Connect all files in the app to the appropriate gems and each other
│         Loads Bundler and all the gems in the Gemfile and the app directory
├── config.ru
│     Loads application environment, code, and libraries
│     Specifies which controllers to load as part of our application using run or use
├── public (front-end assets)
│   └── stylesheets (css, javascript, image files, etc)
└── spec (tests)
    ├── controllers
    ├── features
    ├── models
    └── spec_helper.rb

## Routes

All
  ERB: erb :filename
    Set layout: :layout => path (or false)
Get
  Def: get '/path' do <br> body <br> end
  Dynamic routes: get '/:var' do <br> @var = params[:var] <br> end
Post
  Def: get '/path' do <br> body <br> end
  Parameters: set parameter to instance variable that can be accessed in view.erb
Forms
  Set method="POST" and action="/path" in form tags
  Set name="name" in in input tags: "name" will be the key for params hash
  For nested forms, use name="hash[:group][][:name]"
  Set name="submit" value="submit" in input tags for submit button
  For text area, set name="name" for textarea tags
Layout
  In layout.erb: <%= yield %> to other .erb files where you want to yield

## Active Record

Set up
  Gems (main): 'activerecord', '4.2.5' and 'sinatra-activerecord'
  Gems (:development):'tux' and 'sqlite3'
  Connect to database (environment.rb):
    configure :development do
      set :database, 'sqlite3:db/database_name.db'
    end
  Rakefile: require './config/environment' and 'sinatra/activerecord/rake'
  Multiple controllers: run First_app, use The_rest
Create
  In controller.rb:
    get '/model/new' do
      erb :new
    end
    post '/models' do
      @model = Model.create(attr: params[:attr])
      erb :show
    end
  In new.erb: has form with method="POST" and action="/models"
Read
  In controller.rb:
    get '/models' do
      @models = Model.all
      erb :index
    end
    get '/models/:id' do
      @model = Model.find(params[:id])
      erb :show
    end
  In index.erb: render all of the instances stored in the @models
Update
  In controller.rb:
    get 'models/:id/edit' do
      erb :edit
    end
    patch '/models/:id' do
      @model = Model.find(params[:id])
      @model.update(attr: params[:attr])
      redirect "/models/#{@model.id}"
    end
  In edit.erb: add <input id="hidden" type="hidden" name="(DELETE THE BACKSLASH)\_method" value="patch"> to original form
  In config.ru: use Rack::MethodOverride and run ApplicationController
Delete
  In controller.rb:
    post '/models/:id/delete' do
      redirect '/models'
    end
  In show.erb:
    <form method="post" action="/models/<%= @model.id %>/delete">
      <input id="hidden" type="hidden" name="(DELETE THE BACKSLASH)\_method" value="DELETE">
      <input type="submit" value="delete">
    </form>
