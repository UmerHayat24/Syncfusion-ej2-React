---
title: " Chart Getting Started | React "

component: "Chart"

description: "Getting started file explains how to configure and install chart packages and also how to create basic chart, module injections."
---
<!-- markdownlint-disable MD036 -->

# Getting Started

This section explains you the steps required to create a simple chart and demonstrate the basic usage of the chart control.

To get start quickly with React Charts, you can check on this video:

`youtube:w1xHn0CceqE`

## Dependencies

Below is the list of minimum dependencies required to use the chart component.

```javascript

|-- @syncfusion/ej2-react-charts
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-charts
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-pdf-export
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-compression
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

## Add Chart to the Project

Now, you can start adding Chart component in the application.
For getting started, add the Chart component in `src/App.tsx` file using following code.

{% tab compileJsx=true%}

```tsx

import { ChartComponent } from '@syncfusion/ej2-react-charts';
import * as React from 'react';

class  App  extends  React.Component  {

  render() {
    return  (<ChartComponent />);
  }

}
export  default  App;

```

{% endtab %}

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```

he below example shows a basic Chart.

{% tab template="chart/getting-started/initialize", sourceFiles="app/**/*.tsx",  isDefaultActive=true, compileJsx=true %}

```tsx
import { ChartComponent  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  render() {
    return <ChartComponent id='charts' />
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

* `LineSeries` - Inject this module in to `services` to use line series.
* `Legend` - Inject this module in to `services` to use legend feature.
* `Tooltip` - Inject this module in to `services` to use tooltip feature.
* `DataLabel` - Inject this module in to `services` to use datalabel feature.
* `Category`  - Inject this module in to `services` to use category feature.

These modules should be injected to the `services` section as follows,

 {% tab compileJsx=true%}

```tsx
import { Category, ChartComponent, DataLabel, LineSeries, Legend, Tooltip } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category]} />
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Populate Chart with Data

This section explains how to plot below JSON data to the chart.

{% tab compileJsx=true%}

```tsx
export let data: any[] = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
            ];

```

{% endtab %}

 Add a series object to the chart by using [`series`](../api/chart/seriesModel/) property. Now map the field names `month` and `sales` in the JSON data to the [`xName`](../api/chart/seriesModel/#xname) and
[`yName`](../api/chart/seriesModel/#yname) properties of the series, then set the JSON data to [`dataSource`](../api/chart/seriesModel/#datasource) property.

Since the JSON contains category data, set the [`valueType`](../api/chart/axisModel/#valuetype)for horizontal axis to `Category`. By default, the axis valueType is `Numeric`.

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import { AxisModel, Category,ChartComponent, ColumnSeries, Inject, LineSeries, SeriesCollectionDirective, SeriesDirective, Tooltip  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id="charts" primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Tooltip, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

The sales data are in thousands, so format the vertical axis label by adding
`$` as a prefix and `K` as a suffix to each label. This can be achieved by setting the
`${value}K` to the [`labelFormat`](../api/chart/axisModel/#labelformat) property of axis. Here, `{value}` act as a placeholder
for each axis label.

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import { AxisModel, Category,ChartComponent, ColumnSeries, Inject, LineSeries, SeriesCollectionDirective, SeriesDirective, Tooltip  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = { labelFormat: '${value}K' };

  render() {
    return <ChartComponent id="charts" primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries, Tooltip, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Add Chart Title

You can add a title using [`title`](../api/chart/chartModel/#title) property to the chart to provide
quick information to the user about the data plotted in the chart.

{% tab template="chart/getting-started/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import { AxisModel,Category,ChartComponent, ColumnSeries, Inject, LineSeries, SeriesCollectionDirective, SeriesDirective, Tooltip  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id="charts" primaryXAxis={this.primaryxAxis}
      title='Sales Analysis'>
      <Inject services={[ColumnSeries, Tooltip, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Enable Legend

You can use legend for the chart by setting the `visible` property to true in [`legendSettings`](../api/chart/legendSettingsModel/#visible) object and by injecting the `Legend` module into the `services`.

{% tab template="chart/getting-started/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {AxisModel, Category,ChartComponent, ColumnSeries, Inject, Legend, LegendSeriesModel,
LineSeries, SeriesCollectionDirective, SeriesDirective, Tooltip  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public legendSettings: LegendSeriesModel = { visible: true };
  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id="charts" primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}>
      <Inject services={[ColumnSeries, Tooltip, Legend, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Add Data Label

You can add data labels to improve the readability of the chart.
This can be achieved by setting the visible property to true in the `dataLabel` object  and by injecting `DataLabel` module into the `services`.

{% tab template="chart/getting-started/datalabel", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import { AxisModel,Category,ChartComponent, ColumnSeries, DataLabel, Inject, Legend,
LegendSeriesModel, LineSeries, SeriesCollectionDirective, SeriesDirective, Tooltip  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryyAxis: AxisModel = { labelFormat: '${value}K' };
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public legendSettings: LegendSeriesModel = { visible: true };
  public marker = { dataLabel: { visible: true } };

  render() {
    return <ChartComponent id="charts" primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries, DataLabel, Tooltip, Legend, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' name='Sales' marker={this.marker} />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Enable Tooltip

The tooltip is useful when you cannot display information by using the data labels
due to space constraints. You can enable tooltip by setting the enable property as true in [`tooltip`](../api/chart/tooltipSettingsModel/#enable) object and by injecting `Tooltip` module into the `services`.

{% tab template="chart/getting-started/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import { AxisModel,Category,ChartComponent, ColumnSeries, DataLabel, Inject,
 Legend, LegendSeriesModel, LineSeries, SeriesCollectionDirective, SeriesDirective, Tooltip,TooltipSettingsModel  } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public tooltip: TooltipSettingsModel = { enable: true, shared: false }
  public primaryyAxis: AxisModel = { labelFormat: '${value}K' }
  public primarxyAxis: AxisModel = { valueType: 'Category' }
  public legendSettings: LegendSeriesModel = { visible: true }
  public marker = { dataLabel: { visible: true } };

  render() {
    return <ChartComponent id="charts" primaryXAxis={this.primarxyAxis}
      legendSettings={this.legendSettings}
      primaryYAxis={this.primaryyAxis} tooltip={this.tooltip}>
      <Inject services={[ColumnSeries, DataLabel, Tooltip, Legend, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' name='Sales' marker={this.marker} />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

> You can refer to our [React Charts](https://www.syncfusion.com/react-ui-components/react-charts) feature tour page for its groundbreaking feature representations. You can also explore our [React Charts example](https://ej2.syncfusion.com/react/demos/#/material/chart/line) that shows various chart types and how to represent time-dependent data, showing trends in data at equal intervals.