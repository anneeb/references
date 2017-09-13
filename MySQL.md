# MySql

## Basics

Set up (terminal)
  Open: mysql -uroot
Databases
  Show all databases: show databases;
  See current database: select database();
  Use database: use [name];
  Create database: create database [name];
Tables
  Show tables: show tables;

## Connection

Create connection
  Define: mysql.createConnection({
    host: 'host',
    port: 'port',
    user: 'user',
    database: 'database'
  })
