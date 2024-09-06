---
title: "ContextMenu Getting Started"
component: "ContextMenu"
description: "This section helps to learn how to create the ContextMenu in React application with its basic features in step-by-step procedure."
---
# Getting Started

This section explains how to create a simple ContextMenu, and configure its available functionalities in React

## Dependencies

The following list of dependencies are required to use the ContextMenu component in your application.

```javascript
|-- @syncfusion/ej2-react-navigations
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-base
        |-- @syncfusion/ej2-data
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Setup your development environment

You can use [`Create-react-app`](https://github.com/facebookincubator/create-react-app) to setup
the applications. To install `create-react-app` run the following command.

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

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.

To install `ContextMenu` component, use the following command

```bash
npm install @syncfusion/ej2-react-navigations --save
```

The above command installs [ContextMenu dependencies](./getting-started#dependencies)
which are required to render the component in the `React` environment.

## Adding Style sheet to the Application

Add ContextMenu component's styles as given below in `App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-lists/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";

/* Context Menu target */

#target {
    border: 1px dashed;
    height: 150px;
    padding: 10px;
    position: relative;
    text-align: justify;
    color: gray;
    user-select: none;
}

```

## Add ContextMenu to the project

Now, you can add `ContextMenu` component in the application
For getting started, add `ContextMenu` component in `src/App.tsx` file and the options contain
`menuItems` and `target` in which ContextMenu will be opened. Using the following code snippet.

{% tab compileJsx=true%}

```tsx

import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import './App.css';

class App extends React.Component<{}, {}> {
  private menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];

  public render() {
    return (
      // specifies the tag to render the ContextMenu component
      <div>
        <div id="target">Right click / Touch hold to open the ContextMenu</div>
        <ContextMenuComponent target="#target" items={this.menuItems} />
      </div>
    );
  }
}
```

{% endtab %}

## Run the application

Run the application in the browser using the following command:

```cmd
npm start
```

The following example shows a basic ContextMenu component.

{% tab template= "context-menu/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component {
  private menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];

  public render() {
    return (
            <div className="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target'
              items={this.menuItems}/>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## See Also

* [ContextMenu with icons](./icons-and-navigation#icons)
* [Multi-level nesting](./template#multilevel-nesting)