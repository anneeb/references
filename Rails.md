# Rails

## Basics

Set up (terminal)
  Install rails gem: gem install rails
  Don't make tests: --skip-test-framework
  Create a new file structure: rails new application -d database (defaults to SQLite3)
  Create database: rails db:create
Commands
  List all routes: rake routes
  List all routes for given controller: rake routes | grep model
  Start rails server: rails s
  Start rails console: rails c
Helpers
  Define: helper
  Pluralize: pluralize(number, "thing")
Partials
  Define: (DELETE THE BACKSLASH)\_partial.html.erb
  To include: <%= render 'partial' %>
Flash
  Set up (layout.html.erb):
    <% flash.each do |name, msg| -%>
      <%= content_tag :div, msg, class: name %>
    <% end -%>
  Setting a message: flash[:key] = value
  Colors: :warning, :info, :danger, :success

## Routes, Controllers, and Resources

Routes
  Custom routes: get '/resource', to: 'controller#method', as: 'alias'
  Dynamic routes: resources :controller, only: :method, except: method
  Nested routes: route do more_routes end
Controller
  Explicit render: render "page"
  Redirect: redirect_to alias_path(object)
URL helpers
  Path: resource_path(object)
  Links: link_to object.name, resource_path(object)
  Delete: <%= link_to "Delete", object, method: :delete, data: { confirm: "Are you sure?" } %>

## Forms

Form tag
  Define: <%= form_tag resource_path, method: "verb" do %> ... <% end %>
  Text field: <%= text_field_tag :name, value %>
  Text area:  <%= text_area_tag :name, value %><br>
  Authenticity token: <%= hidden_field_tag :authenticity_token, form_authenticity_token %>
  Submit: <%= submit_tag "value" %>
Form for
  Define: <%= form_for(@object) do |f| %> ... <% end %>
  Label: <%= f.label :name %>
  Text field: <%= f.text_field :name %>
  Text area: <%= f.text_area :name %>
  Number field: <%= f.number_field :name %>
  Select: <%= f.model_select :model_ids, Model.all, :value, :name %>
  Checkboxes: <%= f.collection_check_boxes :model_ids, Model.all, :value, :name %>
  Submit: <%= f.submit %>
  In controller, use: @object.update(params.require(:object))
Strong params
  In config/application.rb: remove config.action_controller.permit_all_parameters = true
  Require: params.permit(:key)
    The params hash must contain a specific key
  Permit: params.permit(:key)
    The params hash may have whatever keys are in it
  Helper method:
    def post_params((DELETE THE BACKSLASH)\*args)
	   params.require(:post).permit(args)
	  end
Nested forms
  Define: <%= f.fields_for :models do |mod| %> ... <% end %>
  Label: <%= mod.label :name %>
  Text field: <%= mod.text_field :name %>
  In the model: accepts_nested_attributes_for :models
Join model forms
  Define: <%= f.fields_for :models, object.models.build do |models_fields| %> ... <% end %>
  Label: <%= models_fields.label :name %>
  Text field: <%= models_fields.text_field :name %>
  In the model: accepts_nested_attributes_for :models
  Helper method:
    def models_attributes=(model_attributes)
      model_attributes.values.each do |model_attribute|
        model = Model.find_or_create_by(model_attribute)
        self.models << model
      end
    end

## Generators

General
  Define: rails g <name of generator>
  Don't make tests: --no-test-framework
Migrations
  Define: migration
  Add column: AddColumn_nameToTable_name column_name:data_type column_name:data_type
    └── db/migrate/timestamp_add_column_name_to_table_name.rb
  Remove column: RemoveColumn_nameFromTable_name column_name:data_type
  Rename column: RenameColumn_nameToColumn_nameInTable
Models
  Define: model
  Create: name column_name:data_type column_name:data_type
    ├── db/migrate/timstamp_create_names.rb
    ├── app/models/name.rb
    ├── spec/models/name_spec.rb
    └── spec/factories/names.rb
  Delete: rails d model name
Controllers
  Define: controller
  Create: name route
    ├── app/controllers/name_controller.rb
    │   └── get 'name/route'
    ├── app/views/names
    │   └── route.html.erb
    ├── app/assets/javascripts/name.coffee
    ├── app/assets/stylesheets/name.scss
    ├── app/helpers/name_helper.rb
    ├── spec/controllers/names_controller_spec.rb
    ├── spec/views/name
    │   └── route.html.erb_spec.rb
    └── spec/helpers/names_helper_spec.rb
  Delete: rails d controller name
Resources
  Define: resource
  Create: Name attribute_name:data_type
    ├── db/migrate/timstamp_create_names.rb
    ├── app/models/name.rb
    ├── app/views/names
    ├── app/controllers/name_controller.rb
    │   └── resources :names
    ├── app/helpers/name_helper.rb
    ├── app/assets/javascripts/name.coffee
    ├── app/assets/stylesheets/name.scss
    ├── spec/models/name_spec.rb
    ├── spec/factories/names.rb
    ├── spec/controllers/names_controller_spec.rb
    └── spec/helpers/names_helper_spec.rb
  Delete: rails d resource Name

## Cookies and Sessions

Cookies
  Set cookie: cookies[:thing] = "value"
  Set cookie with expiration: cookies[:thing] = {value: "value", expires: date}
  See cookies: cookies.inspect
  Delete cookie: cookies.delete[:thing]
Sessions
  Stored in server, specific to the application
  Set object id: session[:object_id] = @object.id
  Load object of a session: @object = session[:object_id]
  Delete session: session.delete(:key)
  Make session or session info available to views (application controller):
    helper_method :method
    def method <stuff with sessions> end
  Routes: new, create, destroy + login to sessions#new
  Views: new (login)
Sessions controller methods
  New: render views for login page
  Create: sets session key-value pairs to form values
    user = User.find_by_email(params[:email])
    if user && user.authenticate(params[:password])
      session[:user] = user
      redirect_to root_path, notice: "logged in!"
    else
      flash.now.alert = "invalid login credentials"
      render "new"
    end
  Destroy: deletes the session key-value pair
    session.delete(:user)
    redirect_to root_path, notice: "logged out!"
Helper methods (application controller)
  Set up: helper_method :method (allows to use helper method through views)
  Current user: @current_user ||= User.find(session[:user_id]) if session[:user_id]
  Logged in: !!current_user

## Authentication

Hashing
  Custom: input.bytes.reduce(:+)
  Salting: number of times running hashing algorithm
Try method
  Define: object.try(:method) == if object != nil then object.method else nil
Set up
  In gemfile: uncomment out bcrypt, looks for column named password_digest
  In form_for: <%= f.password_field :name %>
Controller methods
  Before action: before_action :private_method, [options]
  Has secure password: has_secure_password with password_digest column
  Password confirmation: validates :password_confirmation, presence: true
Class methods
  Set password: object.password
  Authenticate: object.authenticate("string")
    If true -> object
    If false -> false
  Password conformation: object.password_confirmation("string")
    If match -> can use object.save
    If false -> cannot use object.save

## APIs

Simple Internal endpoint
  In routes.rb,
    get 'route', to: controller#action
  In controller.rb,
    def action
      render plain: text
    end
  In page.html.erb,
    <script type="text/javascript">
      $(function () {
        $(".js-button").on('click', function() {
          $.get("route", function(data) {
            $('#target').text(data);
          })
        })
      })
    </script>
