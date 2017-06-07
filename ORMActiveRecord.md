# ORM and Active Record

## ORM: Basics

General
  Connect ruby to a given database:
    database_connection = SQLite3::Database.new('db/database.db')
    database_connection.execute("Some SQL statement")
  Heredoc: create a string that runs on multiple lines
    Def: <<- + name of language contained in our multiline statement + the string, on multiple lines + name of language
Creating the database (environment.rb)
  Require SQLite: require 'sqlite3'
  Require class.rb: require_relative '../lib/app.rb'
  Connect to database: DB = {:conn => SQLite3::Database.new("db/database.db")}
  Return select statements as a hash with column names as keys: DB[:conn].results_as_hash = true
Creating and populating the table (class.rb)
  Accessors and initializing:
    attr_accessor :value, :id

    def initialize(value, id=nil)
      @id = id
      @value = value
    end
  Creating the table:
    def self.create_table
      sql = <<-SQL
      CREATE TABLE IF NOT EXISTS table (
        id INTEGER PRIMARY KEY,
        value TEXT,
        )
      SQL
      DB[:conn].execute(sql)
    end
  Inserting data with save:
    def save
      sql = <<-SQL
        INSERT INTO table (value)
        VALUES (?)
      SQL
      DB[:conn].execute(sql, self.value)
      @id = DB[:conn].execute("SELECT last_insert_rowid() FROM table")[0][0]
    end
  Inserting data with create:
    def self.create(value:)
      new_value = Class.new(value)
      new_value.save
      new_value
    end
  Create new objet from database:
    def self.new_from_db(row)
      new_object = self.new
      new_object.id = row[0]
      new_object.attribute = row[1]
    end
  Import all from database (all):
    def self.all
      sql = <<-SQL
        SELECT *
        FROM songs
        SQL
      DB[:conn].execute(sql).map do |row|
        self.new_from_db(row)
      end
    end
  Find by value:
    def self.find_by_value(value)
      sql = <<-SQL
        SELECT *
        FROM table
        WHERE column_name = ?
        LIMIT 1
        SQL
      DB[:conn].execute(sql, value).map do |row|
        self.new_from_db(row)
      end.first
    end
  Update value:
    def update
      sql = "UPDATE table SET column = ?"
      DB[:conn].execute(sql, self.attribute)
    end
  Insert or update data with save:
    def save
      if self.id
        self.update
      else
        sql = <<-SQL
          INSERT INTO table (value)
          VALUES (?)
        SQL
        DB[:conn].execute(sql, self.value)
        @id = DB[:conn].execute("SELECT last_insert_rowid() FROM table")[0][0]
      end
    end
  Find or create by value:
    def self.find_or_create_by(value:)
      object = DB[:conn].execute("SELECT * FROM table WHERE column_name = ?", value)
      if !object.empty?
        object_data = object[0]
        object = Class.new(object_data[0], object_data[1])
      else
        object = self.create(value: value)
      end
      object
    end

## Dynamic ORM

Table name:
  def self.table_name
    self.to_s.downcase.pluralize
  end
  (for pluralize, require "active_support/inflector" in environment.rb)
Column names:
  def self.column_names
    DB[:conn].results_as_hash = true
    sql = "PRAGMA table_info('#{table_name}')"
    table_info = DB[:conn].execute(sql)
    column_names = []
    table_info.each do |column|
      column_names << column["name"]
    end
    column_names.compact
  end
Attribute accessors:
  self.column_names.each do |col_name|
    attr_accessor col_name.to_sym
  end
Initialize:
  def initialize (options = {})
    options.each do |attribute, value|
      self.send("#{attribute}=", value)
    end
  end
Access table name:
  def table_name_for_insert
    self.class.table_name
  end
Access column names:
  def col_names_for_insert
    self.class.column_names.delete_if {|col| col == "id"}.join(", ")
  end
Access values:
  def values_for_insert
    values = []
    self.class.column_names.each do |col_name|
      values << "'#{send(col_name)}'" unless send(col_name).nil?
      end
    values.join(", ")
  end
Save:
  def save
    sql = "INSERT INTO #{table_name_for_insert} (#{col_names_for_insert}) VALUES (#{values_for_insert})"
    DB[:conn].execute(sql)
    @id = DB[:conn].execute("SELECT last_insert_rowid() FROM #{table_name_for_insert}")[0][0]
  end
Find by name:
  def self.find_by_name(name)
    sql = "SELECT * FROM #{self.table_name} WHERE name = #{name}"
    DB[:conn].execute(sql)
  end

## Active Record: Basics

Setup
  Connect to database:
    connection = ActiveRecord::Base.establish_connection(
      :adapter => "sqlite3",
      :database => "db/database_name.sqlite"
    )
  Create a table using SQL:
    sql = <<-SQL
      CREATE TABLE IF NOT EXISTS songs (
      id INTEGER PRIMARY KEY,
      title TEXT,
      length INTEGER
      )
    SQL
    ActiveRecord::Base.connection.execute(sql)
Methods
  List column names in table: Class.column_names
  Create a new entry in the database: Class.create
  Retrieve an entry from the database by id: Class.find(id)
  Find by any attribute: Class.find_by(attribute: value)
  Get or set attributes: instance.attribute = value
  Save changes to the database: instance.save
Command line
    View available tasks: rake -T
    Call task: rake group_name:task_name
Rakefile
  Grouping tasks:
      namespace :group_name do
        tasks
      end
  Define a task:
      desc "task description"
      task + :task_name do
      end
  Task dependency:
    task :task_name do
      require_relative 'path'
    end
  Migrate:
    namespace :db do
      desc 'migrate changes to your database'
      task :migrate => :environment do
        Class.create_table
      end
    end
  Seed:
    namespace :db do
      desc 'seed the database with some dummy data'
      task :seed do
        require_relative './db/seeds.rb'
      end
    end
  Console:
    desc 'drop into the Pry console'
    task :console => :environment do
      Pry.start
    end
Models (app/models/name.rb)
  Add active record to class: class Name < ActiveRecord::Base
  Belongs to: belongs_to :artist
  Has many: has many :table_name
  Has many through: has many :table_name, through: :table_name
Migrations (db/migrate)
  Define: def change <br> body <br> end
  Create a table:
    create_table :table_name do |t|
      t.data_type :column_name
    end
  Add column to table:
    add_column :table_name, :column_name, :data_type
  Change column:
    change_column :table_name, :column_name, :data_type

## Active Record: Validations

General
  Define: validates :attribute, validator
  Presence: presence: true
  Uniqueness: uniqueness: true
    Scope: { scope: [:attr, :attr], message: "message" }
  Length: length: hash
    Minimum: { minimum: number }
    Maximum: { maximum: number }
    In range: { in: range }
    Is: { is: number }
  Inclusion: inclusion: hash
    In: { in: %w(small medium large) }
  Error message: message: "message"
Custom
  Validate and helper method:
    validate :method
    def method
      if condition
        errors.add(:attribute, "method")
      end
    end
  Validator and validates_with:
    class MyValidator < ActiveModel::Validator
      def validate(record)
        unless condition
          record.errors[:attr] << 'message'
        end
      end
    end
    class Thing
      include ActiveModel::Validations
      validates_with MyValidator
    end
  EachValidator and validates:
    class AttrValidator < ActiveModel::EachValidator
      def validate_each(record, attribute, value)
        unless condition
          record.errors[attribute] << (options[:message] || "message")
        end
      end
    end
    class Person < ApplicationRecord
      validates :attr, presence: true, email: true
    end
Lifecycle Methods
  Define: callback :method
  Before save: before_save
  Before validation: before_validation
  Before create: before_create
