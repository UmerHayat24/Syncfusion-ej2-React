# Getting Started with Syncfusion React UI component in Create React App CLI using NPM/Yarn

Refer the following steps to start using Syncfusion React UI components in React using NPM or Yarn Package Manager.

## Prerequisites

To get started with Syncfusion React UI components, ensure the compatible version of React.

* React versions supported:  Greater than `15.5.4`

* NPM or Yarn Package Manager

## Preparing the application

You can use [`Create-react-app`](https://github.com/facebookincubator/create-react-app) to set up the applications.
To install `create-react-app` run the following command.

For NPM Package Manager,

```bash
npm install -g create-react-app
```

For Yarn Package Manager,

```bash
yarn global add create-react-app
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

All Syncfusion React (Essential JS 2) packages are published on [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install. For this application, we are going to use  Button component.

To install the Button component, use the following command


For NPM Package Manager,

```bash
npm install @syncfusion/ej2-react-buttons --save
```

For Yarn Package Manager,

```bash
 yarn add @syncfusion/ej2-react-buttons
```

## Adding component to the Application

Now, you can start adding required components to the application.
For getting started, we have added Button component in `src/App.tsx` file using the following code.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import './App.css';

export default class App extends React.Component<{}, {}> {
  render() {
    return (
      <ButtonComponent type="primary">Button</ButtonComponent>
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import the Button component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-react-buttons/styles/material.css";
```

## Running the application

Run the application.

For running your application using NPM, use the below command

```bash
npm start
```
For running your application using Yarn, use the below command

```bash
 yarn run start
```

The output will appears as follows.

{% tab template="common/default", isDefaultActive=true compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

//Enable ripple effect
enableRipple(true);

class App extends React.Component<{}, {}> {
  render() {
    return (
      <ButtonComponent>Button</ButtonComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}