---
title: "CheckBox Getting Started"
component: "CheckBox"
description: "This section helps to learn how to create the checkbox in React application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple CheckBox, and configure its available functionalities in React, using React quickstart application.

## Dependencies

The following list of dependencies are required to use the CheckBox component in your application.

```javascript
|-- @syncfusion/ej2-react-buttons
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
```

## Installation and Configuration

You can use [`Create-react-app`](https://github.com/facebookincubator/create-react-app) to setup
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

To install CheckBox component, use the following command

```bash
npm install @syncfusion/ej2-react-buttons --save
```

## Adding CheckBox component to the Application

To include the CheckBox component in your application import the `CheckBoxComponent` from `ej2-react-buttons` package in `App.tsx`.

Add the CheckBox component in application as shown in below code example.

{% tab compileJsx=true%}

```tsx
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import './App.css';
// Import the CheckBox.

// To render CheckBox.
export default class App extends React.Component<{}, {}> {
  render() {
    return (
      <CheckBoxComponent label="Default" />
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import the CheckBox component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
npm start
```

The following example shows a basic CheckBox component.

{% tab template="check-box/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render CheckBox.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <CheckBoxComponent label="Default" />
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}
