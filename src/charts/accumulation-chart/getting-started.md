---
title: " Accumulation Chart Getting Started | React "

component: "Accumulation Chart"

description: "Getting started file explains how configure and install chart packages and also how to create basic accumulation chart."
---
<!-- markdownlint-disable MD036 -->

# Getting Started

In EJ2, accumulation chart is implemented as a separate control to avoid the axis related logics.
The dependencies for accumulation chart is same as chart control.

To get start quickly with React Accumulation Charts, you can check on this video:

`youtube:VHYoL3gVmHA`

## Dependencies

Below is the list of minimum dependencies required to use the accumulation chart component.

```javascript

|-- @syncfusion/ej2-react-charts
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-charts
    |-- @syncfusion/ej2-pdf-export
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-compression
    |-- @syncfusion/ej2-react-popups
    |-- @syncfusion/ej2-react-buttons
    |-- @syncfusion/ej2-react-base
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

## Add Accumulation Chart to the Project

Now, you can start adding Accumulation Chart component in the application.
For getting started, add the Accumulation Chart component in `src/App.tsx` file using following code.

{% tab compileJsx=true%}

```tsx
import {AccumulationChartComponent} from '@syncfusion/ej2-react-charts';
import * as React from 'react';

class  App  extends  React.Component  {

  render() {
    return  (<AccumulationChartComponent />);
  }

}
export default App;

```

{% endtab %}

**Pie Series**

By default, the pie series will be rendered when assigning the JSON data to the series using the
[`dataSource`](../api/accumulation-chart/accumulationSeriesModel/#datasource) property. Map the field names
in the JSON data to the [`xName`](../api/accumulation-chart/accumulationSeriesModel/#xname) and
[`yName`](../api/accumulation-chart/accumulationSeriesModel/#yname) properties of the series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.tsx", compileJsx=true, isDefaultActive=true %}

```tsx
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
    { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
    { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
    { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
    { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];

  render() {
    return <AccumulationChartComponent id="charts">
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' radius='90%' />
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```