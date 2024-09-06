---
title: "Toolbar Getting Started"
component: "Toolbar"
description: "This section explains how to create the Toolbar control in an React application with its basic features."
---

# Getting Started

This section explains you the steps required to create a simple Toolbar and demonstrate the basic usage of the Toolbar control.

## Dependencies

Below is the list of minimum dependencies required to use the Toolbar component.

```javascript
|-- @syncfusion/ej2-react-navigations
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-buttons
        |-- @syncfusion/ej2-popups
```

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

<div class='tsx'>

```sh

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
To install Accordion component, use the following command

```sh
npm install @syncfusion/ej2-react-navigations --save
```

## Adding CSS reference

 Add components style as given below in `src/App.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-navigations/styles/material.css';

```

> To refer `App.css` in the application then import it in the `src/App.tsx` file.

## Initialize the Toolbar with commands

The Toolbar can be rendered by defining an array of [`items`](../api/toolbar#items). An item is rendered with text by defining the default item type as a `Button`.
For more information about item configuration, refer the [Item Configuration](./item-configuration/) section.

* Import the Toolbar component to your `src/App.tsx` file using following code.

{% tab compileJsx=true %}

```typescript
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent id='toolbar'>
        <ItemsDirective>
          <ItemDirective text="Cut" />
          <ItemDirective text="Copy" />
          <ItemDirective text="Paste" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Bold" />
          <ItemDirective text="Italic" />
          <ItemDirective text="Underline" />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

* Now, run the application in the browser using the following command.

```bash
npm start
```

The output will be as follows:

{% tab template="toolbar/toolbar", compileJsx=true, isDefaultActive=true %}

```typescript
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent id='toolbar'>
        <ItemsDirective>
          <ItemDirective text="Cut" />
          <ItemDirective text="Copy" />
          <ItemDirective text="Paste" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Bold" />
          <ItemDirective text="Italic" />
          <ItemDirective text="Underline" />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

## Initialize the Toolbar using HTML elements

The Toolbar component can be rendered based on the given HTML element using `<ToolbarComponent>`.
You need to follow the below structure of HTML elements to render the Toolbar inside the `<ToolbarComponent>` tag.

```html
   <ToolbarComponent>   --> Root Toolbar Element
    <div>      --> Toolbar Items Container
       <div>   --> Toolbar Item Element
       </div>
    </div>
  </ToolbarComponent>
```

{% tab template="toolbar/toolbar-container", compileJsx=true %}

```typescript
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent>
          <div>
              <div><button class='e-btn e-tbar-btn'>Cut</button> </div>
              <div><button class='e-btn e-tbar-btn'>Copy</button> </div>
              <div><button class='e-btn e-tbar-btn'>Paste</button> </div>
              <div class='e-separator'> </div>
              <div><button class='e-btn e-tbar-btn'>Bold</button> </div>
              <div><button class='e-btn e-tbar-btn'>Italic</button> </div>
            </div>
        </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

## See Also

* [How to add Toggle Button](./how-to/add-toggle-button/)