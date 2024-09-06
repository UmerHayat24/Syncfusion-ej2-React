---
title: "ButtonGroup Getting Started"
component: "ButtonGroup"
description: "This section helps to learn how to create the buttongroup in React application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple ButtonGroup, and configure its available functionalities in React by using the React quickstart application.

## Dependencies

The list of dependencies required to use the ButtonGroup component in your application is given below:

```javascript
|-- @syncfusion/ej2-splitbuttons
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

To install ButtonGroup component, use the following command

```bash
npm install @syncfusion/ej2-splitbuttons --save
```

## Adding ButtonGroup component to the Application

To include the ButtonGroup component in your application, add a HTML div tag with class name as `e-btn-group` and to render button
as react component, [`Button dependencies`](./../button/getting-started#dependencies) should be added.

Then import the `ButtonComponent` from `ej2-react-buttons` package and add button
elements that should be group inside the div in `App.tsx`.

Add the ButtonGroup component in application as shown in below code example.

{% tab compileJsx=true%}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import './App.css';
// Import the Button.

// To render ButtonGroup.
export default class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div className='e-btn-group'>
        <ButtonComponent>HTML</ButtonComponent>
        <ButtonComponent>CSS</ButtonComponent>
        <ButtonComponent>Javascript</ButtonComponent>
      </div>
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import the ButtonGroup component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
```

## Running the application

Run the application in the browser by using the following command:

```cmd
npm start
```

The following example shows a basic ButtonGroup component.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className='e-btn-group'>
          <ButtonComponent>HTML</ButtonComponent>
          <ButtonComponent>CSS</ButtonComponent>
          <ButtonComponent>Javascript</ButtonComponent>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));
```

{% endtab %}

## See Also

* [Initialize ButtonGroup using util function](./how-to/initialize-buttongroup-using-util-function)