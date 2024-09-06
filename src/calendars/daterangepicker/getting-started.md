---
title: "Getting Started"
component: "DateRangePicker"
description: "This getting started section briefly explains how to create a date range picker component in an application."
---

# Getting started

This section explains you the steps required to create a simple DateRangePicker and demonstrate the basic usage of the DateRangePicker component.

To get start quickly with React DateRangePicker, you can check on this video:

`youtube:RCC_K6FbZRU`

## Dependencies

The below list of dependencies are required to use the `DateRangePicker` component in your application.

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
You can choose the component that you want to install. For this application, we are going to use `DateRangePicker` component.

To install DateRangePicker component, use the following command

```bash
npm install @syncfusion/ej2-react-calendars –save
```

## Adding Style sheet to the Application

To render the DateRangePicker component, need to import DateRangePicker and its dependent component's styles as given below in `App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-lists/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-calendars/styles/material.css";
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Adding DateRangePicker component to the Application

* To include the DateRangePicker component in application import the `DateRangePickerComponent` from `ej2-react-calendars` package in `App.tsx`.

* Then add the DateRangePicker component as shown in below code example.

`[src/App.tsx]`

```typescript
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import './App.css';

export default class App extends React.Component<{}, {}> {
    public render() {
        return <DateRangePickerComponent id="daterangepicker" />
    }
};
```

## Run the application

Now run the `npm start` command in the console, it will run your application and open the browser window.

```cmd
npm start
```

The below examples shows the basic DateRangePicker component.

{% tab template="daterangepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        return <DateRangePickerComponent id="daterangepicker" placeholder='Select a range' />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Setting the start and end date in a range

The start and end date in a range can be defined with help of
 [`startDate`](../api/daterangepicker#startdate) and [`endDate`](../api/daterangepicker#enddate) property.
The following example demonstrates, how to set the start date, end date on initializing the
DateRangePicker. To know more about range restriction in DateRangePicker, please refer this [page](./range-selection).

{% tab template="daterangepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    private start:Date= new Date("10/7/2017");
    private end:Date= new Date("11/15/2017");

    public render() {
        return <DateRangePickerComponent id="daterangepicker" placeholder='Select a range' startDate={this.start} endDate={this.end} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## See Also

* [Render DateRangePicker with pre-defined ranges](./customization#preset-ranges)
* [Render DateRangePicker with specific culture](./globalization)
