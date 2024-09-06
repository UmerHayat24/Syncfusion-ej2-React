---
title: "Slider Getting Started"
component: "Slider"
description: "Getting started with Slider component."
---

# Getting Started

The following section explains the required steps to build the simple Slider component with its basic usage in step by step procedure.

## Dependencies

Install the below required dependent packages to render the Slider component.

```javascript
|-- @syncfusion/ej2-react-inputs
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-react-popups
    |-- @syncfusion/ej2-react-buttons
    |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-base
        |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-buttons
```

## Installation and Configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
applications.

To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using `create-react-app` command as follows

```bash

create-react-app quickstart --typescript

cd quickstart

```

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in
[`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry. Now, we are going to render
`Slider` component from these packages.

To install `Slider` component, use the following command.

```bash
npm install @syncfusion/ej2-react-inputs --save
```

The above command installs [Slider dependencies](#dependencies)
which are required to render the component in the `React` environment.

## Adding Slider component

Now, you can add `Slider` component in the application.
For getting started, add `Slider` component in `src/App.tsx` file using the following code snippet.

```typescript

import * as React from 'react';
import { SliderComponent } from '@syncfusion/ej2-react-inputs';
import './App.css';

export default class App extends React.Component<{}, {}> {
  render() {
    return (
        <div id='container'>
            <div className='wrap'>
                <SliderComponent id='slider' value={30} />
            </div>
        </div>
    );
  }
}

```

## Adding CSS Reference

Import `Slider` component required theme references at the top of `src/App.css`.

```css

@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-inputs/styles/material.css";

```

> We can also use [CRG](https://crg.syncfusion.com/) to generate combined component styles.

## Run the Application

The Essential JS 2 quickstart application project is configured to compile and run the application in browser. Use the following command to run the application.

```typescript

npm start

```

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  render() {
    return (
        <div id='container'>
            <div className='wrap'>
                <div className="sliderwrap">
                    <SliderComponent id='default' value={30} />
                </div>
            </div>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Types

The types of Slider are as follows:

| **Types** | **Usage** |
| --- | --- |
| Default | Shows a default Slider to select a single value. |
| MinRange | Displays the shadow from the start value to the current selected value. |
| Range | Selects a range of values. It also displays the shadow in-between the selection range. |

>Both the Default Slider and Min-Range Slider have same behavior that is used to select a single value.
In Min-Range Slider, a shadow is considered from the start value to current handle position. But the Range Slider
contains two handles that is used to select a range of values and a shadow is considered in between the two handles.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  render() {
    return (
        <div id='container'>
            <div className='wrap'>
                <div className="sliderwrap">
                    <div className="labeltext">Default</div>
                    <SliderComponent id='default' value={30}/>
                </div>
                <div className="sliderwrap">
                    <div className="labeltext">MinRange</div>
                    <SliderComponent id='minrange' type='MinRange' value={30} />
                </div>
                <div className="sliderwrap">
                    <div className="labeltext">Range</div>
                    <SliderComponent id='range' type='Range' value={[30, 70]} />
                </div>
            </div>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Customization

### Orientation

The Slider can be displayed, either in horizontal or vertical orientation. By default, the Slider renders in horizontal orientation.

{% tab template="slider/orientation", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  render() {
    return (
        <div id='container'>
            <div className='wrap'>
                <SliderComponent id='slider' orientation='Vertical' value={30} />
            </div>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

### Tooltip

The Slider displays the tooltip to indicate the current value by clicking the Slider bar or drag
the Slider handle. The Tooltip position can be customized by using the `placement` property.
Also decides the tooltip display mode on a page, i.e., on hovering, focusing, or clicking on the Slider handle and it always
remains/displays on the page.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*,index.html" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

    public tooltip: Object = { placement: 'After', isVisible: true, showOn: 'Always' };
    render() {
        return (
            <div id='container'>
                <div className='wrap'>
                    <SliderComponent id='slider' type="MinRange"  tooltip={this.tooltip}  value={30} />
                </div>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

### Buttons

The Slider value can be changed by using the Increase and Decrease buttons. In Range Slider, by
default the first handle value will be changed while clicking the button. Change the handle focus and
press the button to change the last focused handle value.

> After enabling the slider buttons if the 'Tab' key is pressed, the focus goes to the handle
and not to the button.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  render() {
    return (
        <div id='container'>
            <div className='wrap'>
                <SliderComponent id='slider' showButtons={true} type='Range' value={[30, 70]} />
            </div>
        </div>
    );
  }
}


ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## See Also

[Slider Formatting](./format)

[Ticks in Slider](./ticks)

[Limits in Slider](./limits)
