# Getting Started

This section explains how to create a simple Chip and to configure the Chip component.

## Dependencies

The list of dependencies required to use the Chip component in your application is given below:

```javascript
|-- @syncfusion/ej2-react-buttons
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-react-base
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

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.

To install Chip component, use the following command

```bash
npm install @syncfusion/ej2-react-buttons --save
```

## Adding Chip component to the Application

To include the Chip component in your application import the `ChipListComponent` from `ej2-react-buttons` package in `App.tsx`.

Add the Chip component in application as shown in below code example.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import './App.css';
// Import the Button.
import { ChipListComponent } from '@syncfusion/ej2-react-buttons';

// To render Button.
export default class App extends React.Component<{}, {}> {
  render() {
    return (
      <ChipListComponent text="Janet Leverling"></ChipListComponent>
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import the Chip component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-react-buttons/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
npm start
```

The following example shows a basic Chip component.

{% tab template="chips/default", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true%}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
      <ChipListComponent text="Janet Leverling"></ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}
