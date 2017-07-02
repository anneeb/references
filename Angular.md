# Angular 4

## Basics

Set Up
  CLI: ng new application
  Quickstart: git clone https://github.com/angular/quickstart.git quickstart
  Remove non-essential files:
    xargs rm -rf < non-essential-files.osx.txt
    rm src/app/*.spec*.ts
    rm non-essential-files.osx.txt

Interpolation: {{}}

## Components

Set up
  Import:
    import { Component, OnInit } from '@angular/core'
  Decorator:
    @Component({
      selector: 'app-name',
      templateUrl: './name.component.html',
      styleUrls: ['./name.component.css']
    })
  Export class:
    export class NameComponent implements OnInit {
      constructor() {}
      ngOnInit() {}
    }

Properties

App
  Properties: prop = value

## Templates



## Generators

General
  Define: ng g <name of generator>
Components
  Define: component
  Create: name
  ├── src/app/name
  │   ├── name.component.css
  │   ├── name.component.html
  │   ├── name.component.spec.ts
  │   └── name.component.ts (required)
  └── src/app/app.module.ts
      ├── import { CompComponent } from './comp/comp.component'
      └── @NgModule({ declarations: [...CompComponent], ... })
