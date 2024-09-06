---
title: "Getting Started For Tooltip"
component: "Tooltip"
description: "Getting started with Tooltip component."
---

# Getting Started

This section briefly explains how to create a simple **Tooltip** component and configure its available functionalities in React.

Tooltips can be initialized on,

* A single element (or)
* A container that has more than one sub-element within it and the sub-elements are considered as targets.

## Dependencies

The following list of dependencies are required to use the Tooltip component in your application.

```javascript
|-- @syncfusion/ej2-react-popups
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-buttons
```

## Installation and configuration

* You can use [`Create-react-app`](https://github.com/facebook/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using `create-react-app` command as follows
<div class='tsx'>

```bash
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

* Install the below required dependency package in order to use the `Tooltip` component in your application.

```bash
npm install @syncfusion/ej2-react-popups --save
```

The above package installs [tooltip dependencies](#dependencies) which are required
 to render the Tooltip component in React environment.

* Tooltip CSS files are available in the `ej2-react-popups` package folder.
Import the Tooltip component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-popups/styles/material.css";
```

> We can also use [CRG](https://crg.syncfusion.com/) to generate combined component styles.

## Initialize the Tooltip on a single element

Import the Tooltip component to your `src/App.tsx` file using following code.

{% tab compileJsx=true%}

```javascript
import * as React from 'react';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';
import './App.css';

export default class App extends React.Component<{}, {}> {
  render() {
    let style: object = {
      display: 'inline-block',
      margin: '60px'
    };
    return (
      <TooltipComponent content="Tooltip Content" style={style}>
        Show Tooltip
      </TooltipComponent>
    );
  }
}

```

{% endtab %}

* Now, run the application in the browser using the following command.

```bash
npm start
```

The output will be as follows:

{% tab template="tooltip/default", isDefaultActive=true, compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
      <div id="container">
        <TooltipComponent position="TopCenter" content="Tooltip Content" target="#target">
          <button className="e-btn" id="target" cssClass="tooltipElement">Show Tooltip</button>
        </TooltipComponent>
      </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));
```

{% endtab %}

## Initialize Tooltip within a container

You can create Tooltips on multiple targets within a container. To do so, you have to define specific target elements to the `target`
 property so that the Tooltip is initialized only on matched targets within a container. In this case, the Tooltip content is assigned from
  the `title` attribute of the target element.

Refer to the following code example to create a Tooltip on multiple targets within a container.

{% tab template="tooltip/multi-target", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true  %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

class App extends React.Component<{}, {}> {
  render() {
    return (
      <div id='container'>
        <TooltipComponent id="details" target='.e-info' position='RightCenter'>
          <form id="details" role="form">
              <table>
                  <tr>
                      <td className="info">User Name</td>
                      <td>
                          <input type="text" className="e-info" name="firstname" title="Please enter your name" /> </td>
                  </tr>
                  <tr>
                      <td className="info">Email Address</td>
                      <td>
                          <input type="text" className="e-info" name="email" title="Enter a valid email address" />
                      </td>
                  </tr>
                  <tr>
                      <td className="info">Password</td>
                      <td>
                          <input type="password" className="e-info" name="password" title="Be at least 8 characters length" />
                      </td>
                  </tr>
                  <tr>
                      <td className="info">Confirm Password</td>
                      <td>
                          <input type="password" className="e-info" name="Cpwd" title="Re-enter your password" />
                      </td>
                  </tr>
                  <tr>
                      <td>
                          <ButtonComponent id="sample" className="center" content="Submit"/>
                      </td>
                      <td>
                          <ButtonComponent id="reset" className="center" content="Reset"/>
                      </td>
                  </tr>
              </table>
          </form>
        </TooltipComponent>
      </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));
```

{% endtab %}

> In the above sample, `details` refers to the container's id, and the target `.e-info` refers to the target elements available
> within that container.

## See Also

[Positioning Tooltip](./position)

[Tooltip Open Mode](./open-mode)

[Customize the Tooltip](./customization)