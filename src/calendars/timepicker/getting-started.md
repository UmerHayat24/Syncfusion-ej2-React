---
title: "Getting Started"
component: "TimePicker"
description: "This getting started section briefly explains how to create a time picker component in an application."
---

# Getting started

This section explains you the steps required to create a simple TimePicker and demonstrate the basic usage of the TimePicker component.

To get start quickly with React TimePicker, you can check on this video:

`youtube:YYu_33pJz9E`

## Dependencies

The below list of dependencies are required to use the `TimePicker` component in your application.

```javascript
|-- @syncfusion/ej2-react-calendars
    |-- @syncfusion/ej2-react-base
        |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-calendars
        |-- @syncfusion/ej2-inputs
            |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install. For this application, we are going to use `TimePicker` component.

To install TimePicker component, use the following command

```bash
npm install @syncfusion/ej2-react-calendars –save
```

## Adding Style sheet to the Application

To render the TimePicker component, need to import TimePicker and its dependent component's styles as given below in `App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-lists/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-calendars/styles/material.css";
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Adding TimePicker component to the Application

* To include the TimePicker component in application import the `TimePickerComponent` from `ej2-react-calendars` package in `App.tsx`.

* Then add the TimePicker component as shown in below code example.

`[src/App.tsx]`

```typescript
import { enableRipple } from '@syncfusion/ej2-base';
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import './App.css';
// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {
    public render() {
        return <TimePickerComponent id="time" />
    }
};

```

## Run the application

Now run the `npm start` command in the console, it will run your application and open the browser window.

```cmd
npm start
```

The following examples shows the basic TimePicker component.

{% tab template="timepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
// import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";
// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {
    public render() {
        return <TimePickerComponent id="timepicker" placeholder="Select a Time" />
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));

```

{% endtab %}

Now, the TimePicker renders with  default culture as `American English`('en-US'). For a different culture, refer to the
[`Globalization`](./globalization/) section.

## Setting the value, min, and max time

The following example demonstrates how to set the value, min and max time on initializing
the TimePicker. Here the TimePicker allows you to select the time value within a range from `7:00 AM` to `4:00 PM`.

{% tab template="timepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
// import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";
// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {

    // initialize the value, min and max time
    private time: Date = (new Date('8/3/2017 10:00 AM'));
    private minTime: Date = (new Date('8/3/2017 7:00 AM'));
    private maxTime: Date = (new Date('8/3/2017 4:00 PM'));

    public render() {
        return <TimePickerComponent id="timepicker" value={this.time} min={this.minTime} max={this.maxTime} />
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));

```

{% endtab %}

## Setting the time format

Time formats is a way of representing the time value in different string format in textbox and popup
list. By default, the TimePicker's format is based on the culture. You can also customize the format by using the
[`format`](../api/timepicker#format)
property. To know more about the time format standards, refer to the
[Date and Time Format](../base/internationalization#custom-formats) section.

The following example demonstrates the TimePicker component in 24 hours format with 60 minutes
interval. The time interval is set to
60 minutes by using the [`step`](../api/timepicker#step) property.

{% tab template="timepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
// import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";
// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {

    private time: Date = (new Date('8/3/2017 10:00'));

    public render() {
        return <TimePickerComponent id="timepicker" value={this.time} step={60} format={'HH:mm'} />
    }
};

ReactDOM.render(<App />, document.getElementById('timer'));

```

{% endtab %}

> Once the time format property is defined, it will be applicable to all the cultures.

## See Also

* [Render TimePicker with min and max time](./time-range)
* [How to achieve validation with TimePicker](./how-to/client-side-validation-using-form-validator)
* [Render TimePicker with specific culture](./globalization)