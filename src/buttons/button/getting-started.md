---
title: "Button Getting Started"
component: "Button"
description: "This section helps to learn how to create the button in React application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple Button and to configure the Button component.

To get start quickly with Button Component using React, you can check on this video:

`youtube:93oXeCB13A0`

## Dependencies

The list of dependencies required to use the Button component in your application is given below:

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

To install Button component, use the following command

```bash
npm install @syncfusion/ej2-react-buttons --save
```

## Adding Button component to the Application

To include the Button component in your application import the `ButtonComponent` from `ej2-react-buttons` package in `App.tsx`.

Add the Button component in application as shown in below code example.

{% tab compileJsx=true%}

```tsx

// Import the Button.
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import './App.css';

// To render Button.
export default class App extends React.Component<{}, {}> {
  public render() {
    return (
      <ButtonComponent>Button</ButtonComponent>
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import the Button component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
npm start
```

The following example shows a basic Button component.

{% tab template="button/default", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Button.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <ButtonComponent>Button</ButtonComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

## See Also

* [Types of Button](./types-and-styles#button-types)