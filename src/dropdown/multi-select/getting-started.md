---
title: "Multiselect Getting started"
component: "MultiSelect"
description: "This section explains how to create a simple Syncfusion react multiselect component and configure its available functionalities in React."
---

# Getting Started

This section explains how to create a simple **MultiSelect** component and configure its available functionalities in React.

## Dependencies

The following list of dependencies are required to use the `MultiSelect` component in your application.

```javascript
|-- @syncfusion/ej2-react-dropdowns
|-- @syncfusion/ej2-react-base
|-- @syncfusion/ej2-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
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

To install MultiSelect component, use the following command

```bash

npm install @syncfusion/ej2-react-dropdowns --save

```

## Adding MultiSelect component

Now, you can start adding MultiSelect component in the application. For getting started, add the
MultiSelect component in `src/App.tsx` file using following code.

Add the below code in the `src/App.tsx` to initialize the MultiSelect.

```typescript

import { MultiSelectComponent  } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public render() {
    return (
       // specifies the tag for render the MultiSelect component
      <MultiSelectComponent  id='mtselement'/>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

## Adding CSS reference

Import the MultiSelect component required CSS references as follows in `src/App.css`.

```css

/* import the MultiSelect dependency styles */

@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-dropdowns/styles/material.css";


```

## Binding data source

After initialization, populate the data using [dataSource](../api/multi-select/#datasource) &nbsp;property.
Here, an array of string values is passed to the MultiSelect component.

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // define the array of data
  private sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics', 'Hockey', 'Rugby', 'Snooker', 'Tennis'];
  public render() {
    return (
        // specifies the tag for render the MultiSelect component
      <MultiSelectComponent id="mtselement" dataSource={this.sportsData} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

## Run the application

After completing the configuration required to render a basic  MultiSelect, run the following command
to display the output in your default browser.

```cmd
npm start
```

{% tab template="multiselect/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // define the array of data
  private sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
  public render() {
    return (
        // specifies the tag for render the MultiSelect component
      <MultiSelectComponent id="mtselement" dataSource={this.sportsData}  placeholder="Find a game" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Configure the Popup List

By default, the width of the popup list automatically adjusts according to the MultiSelect input
element's width and the height of the popup list has '300px'.

You can also customize the suggestion list height and width using
[popupHeight](../api/multi-select/#popupheight)
&nbsp;and [popupWidth](../api/multi-select/#popupwidth) properties
respectively.

In the following sample, popup list's width and height are configured.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics', 'Hockey', 'Rugby','Snooker', 'Tennis'];

    public render() {
        return (
              // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" dataSource={this.sportsData} popupHeight="250px" popupWidth="250px" placeholder="Find a game" />
            );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)