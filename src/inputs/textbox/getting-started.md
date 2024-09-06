---
title: "Getting Started"
component: "Textbox"
description: "Helps to get started with text box component along with its key features such as a floating label, adding icons (input group), and ripple effect."
---

# Getting Started

This section briefly explains about how to create a simple TextBox through CSS classes using `Create React App`.

## Dependencies

The following list of dependencies are required to use the TextBox component in your application.

```javascript
|-- @syncfusion/ej2-react-inputs
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-base
```

## Installation and Configuration

* You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

* Start a new project using create-react-app command as follows.

```bash
create-react-app quickstart --scripts-version=react-scripts-ts
cd quickstart

```

* To install TextBox component, use the following command.

```bash
npm install @syncfusion/ej2-react-inputs –save
```

* The above package installs [Input dependencies](./getting-started/#dependencies)
which are required to render the TextBox component in React environment.

* The TextBox CSS files are available in the `ej2-react-inputs` package folder.
This can be referenced in your application using the following code.

`[src/App.css]`

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-inputs/styles/material.css";
```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Adding TextBox to the application

Return the `HTML input` element with `e-input` class within `render` method in `src/App.tsx` file to render the
TextBox component as like below code.

```typescript
import * as React from "react";
import './App.css';
export default class App extends React.Component<{}, {}> {
    public render() {
      return (
        // element which is going to render the TextBox
        <input className="e-input" type="text" placeholder="Enter Name" />
      );
    }
};

```

## Adding icons to the TextBox

You can create a TextBox with icon as a group by creating the parent div element with the class `e-input-group` and
add the icon element as span with the class `e-input-group-icon`. For detailed information, refer to the [Groups](./groups/) section.

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class Default extends React.Component {

public render() {
   return (
    <div className="e-input-group">
        <input className="e-input" name="input" type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} placeholder="Enter Date"/>
        <span className="e-input-group-icon e-input-popup-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
    </div>
);
}


public onInputFocus(args: React.FocusEvent) {
     ((args.target as HTMLElement).parentElement as HTMLElement).classList.add('e-input-focus');
}

public onInputBlur(args: React.FocusEvent) {
     ((args.target as HTMLElement).parentElement as HTMLElement).classList.remove('e-input-focus');
}


public onIconMouseDown(args: React.MouseEvent) {
    args.persist();
    setTimeout(
        () => {
            (args.target as HTMLElement).classList.add('e-input-btn-ripple');
        },
    300);
}

public onIconMouseUp(args: React.MouseEvent) {
    (args.target as HTMLElement).classList.remove('e-input-btn-ripple');
}
}


ReactDOM.render(<Default />, document.getElementById('input-container'));

```

```html
.e-input-group .e-input-group-icon.e-input-popup-date {
  font-size:16px;
}
.e-input-group-icon.e-input-popup-date:before {
  content: "\e901";
}
```

* Run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="textbox/default", sourceFiles="app/**/*.tsx,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
export default class Default extends React.Component {

public render() {
   return (
    <div className="e-input-group">
        <input className="e-input" name="input" type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} placeholder="Enter Date"/>
        <span className="e-icons e-input-group-icon e-input-popup-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
    </div>
);
}


public onInputFocus(args: React.FocusEvent) {
    ((args.target as HTMLElement).parentElement as HTMLElement).classList.add('e-input-focus');
}

public onInputBlur(args: React.FocusEvent) {
    ((args.target as HTMLElement).parentElement as HTMLElement).classList.remove('e-input-focus');
}


public onIconMouseDown(args: React.MouseEvent) {
    args.persist();
    setTimeout(
        () => {
            (args.target as HTMLElement).classList.add('e-input-btn-ripple');
        },
    300);
}

public onIconMouseUp(args: React.MouseEvent) {
    (args.target as HTMLElement).classList.remove('e-input-btn-ripple');
}
}


ReactDOM.render(<Default />, document.getElementById('input-container'));

```

{% endtab %}

## Floating Label

The floating label TextBox floats the label above the TextBox after focusing, or filled with value in the TextBox.
You can create the floating label TextBox by using the `floatLabelType` API.

{% tab template="textbox/textbox-component", sourceFiles="app/**/index.tsx" %}

```typescript
import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        return (
             <div className="App">
                <div className="textboxes">
                    <h4>FloatLabelType as Auto</h4>
                    <TextBoxComponent placeholder="First Name" floatLabelType="Auto"/>
                </div>
                <div className="textboxes">
                    <h4>FloatLabelType as Always</h4>
                    <TextBoxComponent placeholder="Last Name" floatLabelType="Always"/>
                </div>
            </div>
        )
    }
};
ReactDOM.render(<App />, document.getElementById('input-container'));

```

{% endtab %}

N> You can refer to our [React TextBox](https://www.syncfusion.com/react-ui-components/react-textbox) feature tour page for its groundbreaking feature representations. You can also explore our [React TextBox example](https://ej2.syncfusion.com/react/demos/#/material/textboxes/default) to know how to render and configure the textbox.

## See Also

* [How to render TextBox programmatically](./how-to/add-textbox-programmatically)
* [How to add floating label to TextBox programmatically](./how-to/add-floating-label-to-textbox-programmatically)
