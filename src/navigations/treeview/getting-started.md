---
title: "Getting Started"
component: "TreeView"
description: "Rendering treeview using React"
---

# Getting Started

The following section explains the required steps to build the TreeView component with its basic usage in step by step procedure.

## Dependencies

The following list of dependencies are required to use the `TreeView` component in your application.

```javascript
|-- @syncfusion/ej2-react-navigations
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Installation and configuration

You can use [`Create-react-app`](https://github.com/facebook/create-react-app) to setup the
applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

<div class='tsx'>

```bash

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

## Adding syncfusion packages

All the available Essential JS 2 packages are published in
[`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install.

To install TreeView component, use the following command

```bash
npm install @syncfusion/ej2-react-navigations --save
```

## Adding TreeView component

Now, you can start adding TreeView component in the application. For getting started, add the
TreeView component in `src/App.tsx` file using following code.

Add the below code in the `src/App.tsx` to initialize the TreeView.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import './App.css';
import * as ReactDOM from "react-dom";
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {
  render() {
    return (
       // specifies the tag to render the TreeView component
      <TreeViewComponent></TreeViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('root'));

```

{% endtab %}

## Adding CSS reference

Import the TreeView component required CSS references as follows in `src/App.css`.

```css

/* import the TreeView dependency styles */

@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://ej2crg.azurewebsites.net/) (Custom Resource Generator) in your application.

## Binding data source

TreeView can load data either from local data sources or remote data services. This can be done using the `dataSource` property
that is a member of the [fields](../api/treeview#fields) property. The dataSource property supports
array of JavaScript objects and `DataManager`. Here, an array of JSON values is passed to the TreeView component.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import './App.css';
import * as ReactDOM from 'react-dom';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {
  // define the array of data
  public hierarchicalData: { [key: string]: Object }[] = [
    { id: '01', name: 'Local Disk (C:)', expanded: true,
        subChild: [
            {
                id: '01-01', name: 'Program Files',
                subChild: [
                    { id: '01-01-01', name: '7-Zip' },
                    { id: '01-01-02', name: 'Git' },
                    { id: '01-01-03', name: 'IIS Express' },
                ]
            },
            {
                id: '01-02', name: 'Users', expanded: true,
                subChild: [
                    { id: '01-02-01', name: 'Smith' },
                    { id: '01-02-02', name: 'Public' },
                    { id: '01-02-03', name: 'Admin' },
                ]
            },
            {
                id: '01-03', name: 'Windows',
                subChild: [
                    { id: '01-03-01', name: 'Boot' },
                    { id: '01-03-02', name: 'FileManager' },
                    { id: '01-03-03', name: 'System32' },
                ]
            },
        ]
    },
    {
        id: '02', name: 'Local Disk (D:)',
        subChild: [
            {
                id: '02-01', name: 'Personals',
                subChild: [
                    { id: '02-01-01', name: 'My photo.png' },
                    { id: '02-01-02', name: 'Rental document.docx' },
                    { id: '02-01-03', name: 'Pay slip.pdf' },
                ]
            },
            {
                id: '02-02', name: 'Projects',
                subChild: [
                    { id: '02-02-01', name: 'ASP Application' },
                    { id: '02-02-02', name: 'TypeScript Application' },
                    { id: '02-02-03', name: 'React Application' },
                ]
            },
            {
                id: '02-03', name: 'Office',
                subChild: [
                    { id: '02-03-01', name: 'Work details.docx' },
                    { id: '02-03-02', name: 'Weekly report.docx' },
                    { id: '02-03-03', name: 'Wish list.csv' },
                ]
            },
        ]
    },
    {
        id: '03', name: 'Local Disk (E:)', icon: 'folder',
        subChild: [
            {
                id: '03-01', name: 'Pictures',
                subChild: [
                    { id: '03-01-01', name: 'Wind.jpg' },
                    { id: '03-01-02', name: 'Stone.jpg' },
                    { id: '03-01-03', name: 'Home.jpg' },
                ]
            },
            {
                id: '03-02', name: 'Documents',
                    subChild: [
                    { id: '03-02-01', name: 'Environment Pollution.docx' },
                    { id: '03-02-02', name: 'Global Warming.ppt' },
                    { id: '03-02-03', name: 'Social Network.pdf' },
                ]
            },
            {
                id: '03-03', name: 'Study Materials',
                subChild: [
                    { id: '03-03-01', name: 'UI-Guide.pdf' },
                    { id: '03-03-02', name: 'Tutorials.zip' },
                    { id: '03-03-03', name: 'TypeScript.7z' },
                ]
            },
        ]
    }
];
private fields: Object = { dataSource: this.hierarchicalData, id: 'id', text: 'name', child: 'subChild' };
  render() {
    return (
        // specifies the tag for render the TreeView component
     <TreeViewComponent fields={this.fields} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('root'));

```

{% endtab %}

## Run the application

After completing the configuration required to render a basic TreeView, run the following command to
display the output in your default browser.

```cmd
npm start
```

{% tab template="tree-view/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {
 // define the array of data
  public hierarchicalData: { [key: string]: Object }[] = [
    { id: '01', name: 'Local Disk (C:)', expanded: true,
        subChild: [
            {
                id: '01-01', name: 'Program Files',
                subChild: [
                    { id: '01-01-01', name: '7-Zip' },
                    { id: '01-01-02', name: 'Git' },
                    { id: '01-01-03', name: 'IIS Express' },
                ]
            },
            {
                id: '01-02', name: 'Users', expanded: true,
                subChild: [
                    { id: '01-02-01', name: 'Smith' },
                    { id: '01-02-02', name: 'Public' },
                    { id: '01-02-03', name: 'Admin' },
                ]
            },
            {
                id: '01-03', name: 'Windows',
                subChild: [
                    { id: '01-03-01', name: 'Boot' },
                    { id: '01-03-02', name: 'FileManager' },
                    { id: '01-03-03', name: 'System32' },
                ]
            },
        ]
    },
    {
        id: '02', name: 'Local Disk (D:)',
        subChild: [
            {
                id: '02-01', name: 'Personals',
                subChild: [
                    { id: '02-01-01', name: 'My photo.png' },
                    { id: '02-01-02', name: 'Rental document.docx' },
                    { id: '02-01-03', name: 'Pay slip.pdf' },
                ]
            },
            {
                id: '02-02', name: 'Projects',
                subChild: [
                    { id: '02-02-01', name: 'ASP Application' },
                    { id: '02-02-02', name: 'TypeScript Application' },
                    { id: '02-02-03', name: 'React Application' },
                ]
            },
            {
                id: '02-03', name: 'Office',
                subChild: [
                    { id: '02-03-01', name: 'Work details.docx' },
                    { id: '02-03-02', name: 'Weekly report.docx' },
                    { id: '02-03-03', name: 'Wish list.csv' },
                ]
            },
        ]
    },
    {
        id: '03', name: 'Local Disk (E:)', icon: 'folder',
        subChild: [
            {
                id: '03-01', name: 'Pictures',
                subChild: [
                    { id: '03-01-01', name: 'Wind.jpg' },
                    { id: '03-01-02', name: 'Stone.jpg' },
                    { id: '03-01-03', name: 'Home.jpg' },
                ]
            },
            {
                id: '03-02', name: 'Documents',
                    subChild: [
                    { id: '03-02-01', name: 'Environment Pollution.docx' },
                    { id: '03-02-02', name: 'Global Warming.ppt' },
                    { id: '03-02-03', name: 'Social Network.pdf' },
                ]
            },
            {
                id: '03-03', name: 'Study Materials',
                subChild: [
                    { id: '03-03-01', name: 'UI-Guide.pdf' },
                    { id: '03-03-02', name: 'Tutorials.zip' },
                    { id: '03-03-03', name: 'TypeScript.7z' },
                ]
            },
        ]
    }
];
private fields: object = { dataSource: this.hierarchicalData, id: 'id', text: 'name', child: 'subChild' };
  render() {
    return (
      // specifies the tag for render the TreeView component
     <TreeViewComponent fields={this.fields} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to customize treeview as accordion](./how-to/accordion-tree/)

* [How to set tooltip for treeview nodes](./how-to/set-tool-tip-for-tree-nodes/)

* [How to filter nodes in treeview](./how-to/filtering-tree-nodes/)

* [How to get all the child nodes through parentID](./how-to/get-all-child-nodes/)
