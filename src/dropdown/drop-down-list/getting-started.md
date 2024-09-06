---
title: "Drop-down list Getting started"
component: "DropDownList"
description: "This section explains how to create a simple Syncfusion react drop-down list component and configure it's functionalities."
---

# Getting Started

This section briefly explains how to create a simple **DropDownList** component and configure its available
functionalities in React.

## Dependencies

The following list of dependencies are required to use the `DropDownList` component in your application.

```javascript
|-- @syncfusion/ej2-react-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-dropdowns
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Installation and configuration

You can use [`Create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

```bash

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

## Adding syncfusion packages

All the available Essential JS 2 packages are published in
[`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install.

To install DropDownList component, use the following command

```bash
npm install @syncfusion/ej2-react-dropdowns –save
```

## Adding DropDownList component

Now, you can start adding DropDownList component in the application. For getting started, add the
DropDownList component in `src/App.tsx` file using following code.

Add the below code in the `src/App.tsx` to initialize the DropDownList.

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public render() {
    return (
       // specifies the tag for render the DropDownList component
      <DropDownListComponent id='ddlelement'/>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

## Adding CSS reference

Import the DropDownList component required CSS references as follows in `src/App.css`.

```css

/* import the DropDownList dependency styles */

@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-dropdowns/styles/material.css";

```

## Binding data source

After initialization, populate the DropDownList with data using
the [dataSource](../api/drop-down-list/#datasource) &nbsp;property.
Here, an array of string values is passed to the DropDownList component.

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // define the array of data
  private sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
  public render() {
    return (
        // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" dataSource={this.sportsData} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

## Run the application

After completing the configuration required to render a basic DropDownList, run the following command to
display the output in your default browser.

```cmd
npm start
```

{% tab template="dropdownlist/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // define the array of data
  private sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
  public render() {
    return (
        // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" dataSource={this.sportsData}  placeholder="Select a game" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Configure the Popup List

By default, the width of the popup list automatically adjusts according to the DropDownList input
element's width, and the height of the popup list has '300px'.

The height and width of the popup list can also be customized using the
[popupHeight](../api/drop-down-list/#popupheight)
&nbsp;and [popupWidth](../api/drop-down-list/#popupwidth) properties
respectively.

In the following sample, popup list's width and height are configured.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Hockey', 'Rugby','Snooker', 'Tennis'];

    public render() {
        return (
              // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" dataSource={this.sportsData} popupHeight="200px" popupWidth="250px" placeholder="select a game" />
            );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)