---
title: "Getting Started"
component: "Dashboard Layout"
description: "This section explains how to create a DashboardLayout component in the React application with its basic features."
---

# Getting Started

This section explains how to create a simple **Dashboard Layout** component and its basic usage.

## Dependencies

The following list of dependencies is required to use the Dashboard Layout component in your application.

```js
|-- @syncfusion/ej2-react-layouts
    |-- @syncfusion/ej2-react-base
        |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-layouts

```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

<div class='tsx'>

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

* Install Syncfusion Dashboard Layout package using below command.

```cmd
npm install @syncfusion/ej2-react-layouts --save
```

## Adding Style sheet to the Application

To render the Dashboard Layout component, need to import Dashboard Layout and its dependent component's styles as given below in `App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-layouts/styles/material.css";
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Add Dashboard Layout to the application

You can render the Dashboard Layout component in the following two ways.

* Defined the panels property as the attribute in the HTML element directly.
* Using the `panels` property directly.

## Setting the `panels` property using HTML attributes

You can render the Dashboard Layout component by adding the panels property as the attribute to the HTML element. Add the HTML div element with panel definition for Dashboard Layout into your `App.tsx` file.

`[src/App.tsx]`

{% tab compileJsx=true%}

```typescript
// import the DashboardLayout component
import { DashboardLayoutComponent } from '@syncfusion/ej2-react-layouts';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
  private cellSpacing: number[] = [5, 5];

  public render() {
    return (
      <div>
        <div className="control-section">
          <DashboardLayoutComponent id='defaultLayout' cellSpacing={this.cellSpacing} allowResizing={true} columns={5}>
            <div id="one" className="e-panel" data-row="0" data-col="0" data-sizex="1" data-sizey="1">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">0</div>
              </div>
            </div>
            <div id="two" className="e-panel" data-row="1" data-col="0" data-sizex="1" data-sizey="2">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">1</div>
              </div>
            </div>
            <div id="three" className="e-panel" data-row="0" data-col="1" data-sizex="2" data-sizey="2">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">2</div>
              </div>
            </div>
            <div id="four" className="e-panel" data-row="2" data-col="1" data-sizex="1" data-sizey="1">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">3</div>
              </div>
            </div>
            <div id="five" className="e-panel" data-row="2" data-col="2" data-sizex="2" data-sizey="1">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">4</div>
              </div>
            </div>
            <div id="six" className="e-panel" data-row="0" data-col="3" data-sizex="1" data-sizey="1">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">5</div>
              </div>
            </div>
            <div id="seven" className="e-panel" data-row="1" data-col="3" data-sizex="1" data-sizey="1">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">6</div>
              </div>
            </div>
            <div id="eight" className="e-panel" data-row="0" data-col="4" data-sizex="1" data-sizey="3">
              <span id="close" className="e-template-icon e-clear-icon" />
              <div className="e-panel-container">
                <div className="text-align">7</div>
              </div>
            </div>
          </DashboardLayoutComponent>
        </div>
      </div>
    );
  }
}

```

{% endtab %}

## Run the application

Now, use the `npm start` command to run the application in the browser.

```cmd
npm start
```

The following example shows a basic Dashboard Layout by adding the panels property directly into the HTML element.

{% tab template="dashboard-layout/getting-started",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css"  %}

{% endtab %}

## Setting the `panels` property directly

You can render the Dashboard Layout component by using the **panels** property directly.

`[src/App.tsx]`

{% tab compileJsx=true%}

```typescript
// import the DashboardLayout component
import { DashboardLayoutComponent } from '@syncfusion/ej2-react-layouts';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
  private cellSpacing: number[] = [5, 5];
  private panels: object[] = [
    { "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content: '<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content: '<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content: '<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content: '<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content: '<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content: '<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content: '<div class="content">6</div>' }
  ];

  public render() {
    return (
      <div>
        <div className="control-section">
          <DashboardLayoutComponent id='defaultLayout' cellSpacing={this.cellSpacing} allowResizing={true} panels={this.panels} columns={5} />
        </div>
      </div>
    );
  }
}

```

{% endtab %}

The following example shows a basic Dashboard Layout by using the `panels` property.

{% tab template="dashboard-layout/getting-started-panel",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css" %}

{% endtab %}
