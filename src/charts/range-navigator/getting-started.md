---
title: " RangeNavigator Getting Started | React "

component: "RangeNavigator"

description: "Getting started file explains how to configure and install rangenavigator packages and also how to create basic rangenavigator, module injections."
---

# Getting Started

This section explains you the steps required to create a simple range navigator and demonstrate the basic
usage of the range navigator control.

## Dependencies

The list of minimum dependencies required to use an range navigator are follows:

```javascript

|-- @syncfusion/ej2-react-charts
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-pdf-export
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-compression
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-calendars
    |-- @syncfusion/ej2-svg-base

```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

<div class='tsx'>

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-react-charts --save
```

## Add Range Navigator to the Project

Now, you can start adding range navigator component in the application.
For getting started, add the Chart component in `src/App.tsx` file using following code.

```tsx

import * as React from 'react';
import {RangeNavigatorComponent} from '@syncfusion/ej2-react-charts';

class  App  extends  React.Component  {

  render() {
    return  (<RangeNavigatorComponent></RangeNavigatorComponent>);
  }

};
export default App;

```

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```

The below example shows a basic Range Navigator.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true,  isDefaultActive=true %}

```tsx
import { RangeNavigatorComponent} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class  App  extends  React.Component  {

  render() {
    return <RangeNavigatorComponent id="charts" />
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Module Injection

Chart component are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature service in the AppModule. In the current application, we are
going to modify the above basic chart to visualize sales data for a particular year.
For this application we are going to use line series, tooltip, data label, category axis and legend
feature of the chart. Please find the relevant feature
service name and description as follows.

* `AreaSeries` - Inject this module in to `services` to use area series.
* `DateTime` - Inject this module in to `services` to use date time feature.
* `RangeTooltip` - Inject this module in to `services` to use tooltip feature.

These modules should be injected to the `services` section as follows,

 ```javascript
import { AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangeTooltip} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class  App  extends  React.Component  {

  render() {
    return <RangeNavigatorComponent id='charts'>
      <Inject services={[AreaSeries, DateTime, RangeTooltip]} />
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

 ```

## Populate Range Navigator with Data

Now, we are going to provide data to the range navigator. Add a [`series`](../api/range-navigator/rangeNavigatorSeriesModel/) object to the range navigator
by using series property. Now map the field names x and y in the JSON data to the [`xName`](../api/range-navigator/rangeNavigatorSeriesModel/#xname) and
[`yName`](../api/range-navigator/rangeNavigatorSeriesModel/#yname) properties of the series, then set the JSON data to dataSource property.
Since the JSON contains Datetime data, set the [`valueType`](../api/range-navigator/rangeNavigatorModel/#valuetype) range Navigator to `Category`.
By default, the axis `valueType` is `Numeric`.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip]} />
      <RangenavigatorSeriesCollectionDirective>
        <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
      </RangenavigatorSeriesCollectionDirective>
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Enable Tooltip

The tooltip is useful to show the selected data. You can enable the tooltip by setting the `enable` property as true in
tooltip object and by injecting `RangeTooltip` module into the `services`.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries,  DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip,RangeTooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true, displayMode: 'Always' };

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
      tooltip={this.tooltip}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip]} />
      <RangenavigatorSeriesCollectionDirective>
        <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
      </RangenavigatorSeriesCollectionDirective>
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}