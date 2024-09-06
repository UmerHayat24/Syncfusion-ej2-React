---
title: "ProgressButton Getting Started"
component: "ProgressButton"
description: "This section helps to learn how to create the progressbutton in React application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple ProgressButton and to configure it.

## Dependencies

The list of dependencies required to use the ProgressButton component in your application is given as follows:

```js
|-- @syncfusion/ej2-react-splitbuttons
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
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

```bash

create-react-app quickstart

cd quickstart

```

</div>

> 'react-scripts-ts' is used for creating React app with typescript.

## Adding syncfusion packages

All the available Essential JS 2 packages are published in
[`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install.

To install ProgressButton component, use the following command

```bash
npm install @syncfusion/ej2-react-splitbuttons --save

```

## Adding ProgressButton component

Now, you can start adding ProgressButton component in the application. For getting started, add the
ProgressButton component in `src/App.tsx` file using following code.

Add the below code in the `src/App.tsx` to initialize the ProgressButton.

{% tab compileJsx=true%}

```typescript
import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import './App.css';

// To render ProgressButton.
export default class App extends React.Component<{}, {}> {

  public render() {
    return (
      <div>
        <ProgressButtonComponent content='Spin Left' />
      </div>
    );
  }
}
```

{% endtab %}

## Adding CSS reference

Import the ProgressButton component required CSS references as follows in `src/App.css`.

```css
/* import the ProgressButton dependency styles */
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";

```

## Run the application

After completing the configuration required to render a basic ProgressButton, run the following command to
display the output in your default browser.

```cmd
npm start
```

{% tab template="progress-button/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html, styles.css", compileJsx=true %}

```tsx
import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ProgressButton.
class App extends React.Component<{}, {}> {

  public render() {
    return (
    <div>
      <ProgressButtonComponent content='Spin Left'/>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('progress-button'));
```

{% endtab %}

> ProgressButton supports different styles, types and sizes like [`Button`](https://ej2.syncfusion.com/react/documentation/button/). In addition, it also supports `top` and `bottom` icon positions.

## See Also

* [Spinner and Progress options](spinner-and-progress#spinner)
