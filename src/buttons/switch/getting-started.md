---
title: "Switch Getting Started"
component: "Switch"
description: "This section helps to learn how to create the switch in React application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple Switch, and configure its available functionalities in React, using React quickstart application.

## Dependencies

The following list of dependencies are required to use Switch component in your application.

```javascript
|-- @syncfusion/ej2-react-buttons
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
```

## Installation and Configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup
the applications. To install `create-react-app` run the following command.

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

```bash

create-react-app quickstart

cd quickstart

```

</div>

> 'react-scripts-ts' is used for creating React app with typescript.

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.

To install Switch component, use the following command

```bash
npm install @syncfusion/ej2-react-buttons --save
```

## Adding Switch component to the Application

To include Switch component in your application import the `SwitchComponent` from `ej2-react-buttons` package in `App.tsx`.

Add Switch component in application as shown in below code example.

{% tab compileJsx=true%}

```tsx
// Import the Switch.
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import './App.css';

// To render Switch.
export default class App extends React.Component<{}, {}> {
  public render() {
    return (
      <SwitchComponent />
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import the Switch component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
npm start
```

The following example shows a basic Switch component.

{% tab template="switch/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Switch with checked state.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <SwitchComponent checked={true} />
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}

## See Also

* [How to customize the switch appearance](./how-to/customize-the-appearance-of-a-switch)
