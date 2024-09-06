---
title: "ColorPicker Getting Started"
component: "ColorPicker"
description: "This section helps to learn how to create the color picker in React application with its basic features in step-by-step procedure."
---

# Getting Started

The following section explains the required steps to build the
ColorPicker component with its basic usage in step-by-step procedure.

## Dependencies

The following list of dependencies are required to use the ColorPicker component in your application.

```javascript
|-- @syncfusion/ej2-react-inputs
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-splitbuttons
```

## Installation and configuration

You can use [Create-react-app](https://github.com/facebookincubator/create-react-app) to setup the applications.
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

All the available Essential JS 2 packages are published in [npmjs.com](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install. For this application, we are going to use ColorPicker component.

To install ColorPicker component, use the following command

```bash
npm install @syncfusion/ej2-react-inputs –save
```

## Adding ColorPicker to the application

Now, you can start adding ColorPicker component to the application. We have added ColorPicker component in
`src/App.tsx` file using following code.

{% tab compileJsx=true%}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes ColorPicker component
ReactDOM.render(<ColorPickerComponent/>);

```

{% endtab %}

## Adding CSS reference

Import the ColorPicker component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
```

## Run the application

Use the `npm run start` command to run the application in the browser.

```cmd
npm run start
```

The following example shows the default ColorPicker.

{% tab template="colorpicker/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes ColorPicker component.
class App extends React.Component<{}, {}> {
    public render() {
        return (
           <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent id='color-picker'/>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [Set color value](./mode-and-value#color-value)
* [ColorPicker customization](./how-to/customize-colorpicker)