---
title: "Kanban Getting Started"
component: "Kanban"
description: "This article demonstrates how to create a simple Kanban and configure its available features."
---

# Getting Started

This section briefly explains how to create **Kanban** component and configure its available functionalities in React environment,
using Essential JS 2 [quickstart](https://github.com/syncfusion/ej2-quickstart.git) seed repository.

## Dependencies

The following list of dependencies are required to use the Kanban component in your application.

```tsx
|-- @syncfusion/ej2-react-kanban
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-kanban
        |-- @syncfusion/ej2-layouts
        |-- @syncfusion/ej2-navigations
          |-- @syncfusion/ej2-inputs
            |-- @syncfusion/ej2-splitbuttons
          |-- @syncfusion/ej2-lists
          |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Installation and configuration

### Setup for local development

You can use create-react-app to setup the applications. To install create-react-app run the following command.

```sh
npm install -g create-react-app
```

To setup basic React sample use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts
cd quickstart
```

```sh
create-react-app quickstart
cd quickstart
```

### Adding Syncfusion packages

All the available Essential JS 2 packages are published in `npmjs.com` public registry. To install Kanban component, use the following command.

```sh
npm install @syncfusion/ej2-react-kanban --save
```

### Adding CSS reference

Add Kanban component's styles as given below in `src/App.css`.

```sh
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import "../node_modules/@syncfusion/ej2-layouts/styles/material.css";
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-kanban/styles/material.css";
```

>To refer `App.css` in the application then import it in the `src/App.tsx` file.

In case, if you want to make use of the combined CSS files of entire components,
then you can avail it from the root folder of Essential JS 2 package and reference it with the code shown below.

```css
@import '../../node_modules/@syncfusion/ej2/material.css';
```

## Initialize the Kanban

Add the HTML div tag defined with an `id` attribute in your `index.html` file, where the kanban element is initialized.

`[src/index.html]`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Syncfusion React Kanban</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Essential JS 2 for React Components" />
    <meta name="author" content="Syncfusion" />
    <link href="//cdn.syncfusion.com/ej2/ej2-react-kanban/styles/material.css" rel="stylesheet" />
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/systemjs/0.19.38/system.js"></script>
    <script src="systemjs.config.js"></script>
     <style>
        #loader {
            color: #008cff;
            height: 40px;
            left: 45%;
            position: absolute;
            top: 45%;
            width: 30%;
        }
    </style>
</head>
<body>
    <!--Element where the Kanban will be rendered-->
    <div id="kanban"></div>
</body>
</html>
```

Import the Kanban component to your `app.tsx` file as shown below,
and initialize it to the element defined with an id `kanban` in the `index.html` file.

{% tab template="kanban/getting-started-empty", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-react-kanban";

class App extends React.Component<{}, {}>{
  render() {
    return <KanbanComponent id="kanban" keyField="Status">
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" />
                  <ColumnDirective headerText="Testing" keyField="Testing" />
                  <ColumnDirective headerText="Done" keyField="Close" />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}

Now, run the application in the browser using the following command.

```sh
npm start
```

The output will display the kanban header.

## Populating cards

To populate the empty Kanban with cards, define the local JSON data or remote data using the `dataSource` property. To define `dataSource`, the mandatory fields in JSON object should be relevant to `keyField`. In the following example, you can see the cards defined with default fields such as ID, Summary, and Status.

{% tab template="kanban/getting-started-key-field", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-react-kanban";
import { kanbanData } from './datasource';

class App extends React.Component<{}, {}>{
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
    }
  render() {
    return <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }}>
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" />
                  <ColumnDirective headerText="Testing" keyField="Testing" />
                  <ColumnDirective headerText="Done" keyField="Close" />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}

## Enable swimlane

`Swimlane` can be enabled by mapping the fields `swimlaneSettings.keyField` to appropriate column name in dataSource. This enables the grouping of the cards based on the mapped column values.

{% tab template="kanban/getting-started-swimlane", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-react-kanban";
import { kanbanData } from './datasource';

class App extends React.Component<{}, {}>{
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
    }
  render() {
    return <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} swimlaneSettings={{ keyField: "Assignee" }}>
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" />
                  <ColumnDirective headerText="Testing" keyField="Testing" />
                  <ColumnDirective headerText="Done" keyField="Close" />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}
