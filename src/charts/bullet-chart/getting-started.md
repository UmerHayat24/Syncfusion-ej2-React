---
title: "Bullet Chart Getting Started | React "

component: "Bullet Chart"

description: "Getting started file explains how to configure and install chart packages and also how to create basic bullet chart, module injections."
---

<!-- markdownlint-disable MD036 -->

# Getting Started

This section explains you the steps required to create a simple Bullet Chart and demonstrate the basic usage of the Bullet Chart control.

## Dependencies

Below is the list of minimum dependencies required to use the Bullet Chart component.

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

To setup basic `React` sample use following commands.

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

Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-react-charts --save
```

## Add Bullet Chart to the Project

Now, you can start adding Bullet Chart component in the application.
For getting started, add the Bullet Chart component in `src/App.tsx` file using following code.

{% tab compileJsx=true%}

```tsx
import { BulletChartComponent } from "@syncfusion/ej2-react-charts";
import * as React from "react";

class App extends React.Component {
  render() {
    return <BulletChartComponent />;
  }
}
export default App;
```

{% endtab %}

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```

The below example shows a basic Bullet Chart.

{% tab template="bullet-chart/getting-started/initialize", sourceFiles="app/**/*.tsx",  isDefaultActive=true, compileJsx=true %}

```tsx
import { BulletChartComponent } from "@syncfusion/ej2-react-charts";
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
    return <BulletChartComponent id="bulletChart" />;
  }
}
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Module Injection

Bullet Chart are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature service in the AppModule. Please find the relevant feature
service name and description as follows.

* `BulletTooltip` - Inject this module in to `services` to use tooltip feature.

These modules should be injected to the `services` section as follows,

{% tab compileJsx=true%}

```tsx
import {
  BulletChartComponent,
  BulletTooltip
} from "@syncfusion/ej2-react-charts";
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
    return (
      <BulletChartComponent id="bulletChart">
        <Inject services={[BulletTooltip]} />
      </BulletChartComponent>
    );
  }
}
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Bullet Chart With Data

This section explains how to plot local data to the Bullet Chart.

{% tab compileJsx=true%}

```tsx
let data: any[] = [
  { value: 100, target: 80 },
  { value: 200, target: 180 },
  { value: 300, target: 280 },
  { value: 400, target: 380 },
  { value: 500, target: 480 }
];
```

{% endtab %}

Now assign the local data to `dataSource` property. **value** and **target** values should be mapped with `valueField` and `targetField` respectively.

{% tab template="bullet-chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{

  public data: any[] = [
       { value: 100, target: 80 },
       { value: 200, target: 180 },
       { value: 300, target: 280 },
       { value: 400, target: 380 },
       { value: 500, target: 480 },
  ];

  render() {
    return (<BulletChartComponent id='Revenue'
                        style={{ textAlign: "center" }}
                        animation={{ enable: false }}
                        valueField='value'
                        targetField='target'
                        minimum={0}
                        maximum={300}
                        interval={50}
                        dataSource={this.data}>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Add Bullet Chart Title

You can add a title using `title` property to the Bullet Chart to provide quick
information to the user about the data plotted in the Bullet Chart.

{% tab template="bullet-chart/getting-started/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='title'
                        style={{ textAlign: "center" }}
                        animation={{ enable: false }}
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={300}
                        interval={50}
                        dataSource={[{value: 270, target: 250}]}>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Ranges

You can add a range using `BulletRangeCollectionDirective` and `BulletRangeDirective` directives of the Bullet Chart.

{% tab template="bullet-chart/getting-started/ranges", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                        style={{ textAlign: "center" }}
                        animation={{ enable: false }}
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={300}
                        interval={50}
                        dataSource={[{value: 270, target: 250}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={100} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={200} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={300} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Tooltip

You can use tooltip for the Bullet Chart by setting the `enable` property to true in `tooltip` object and by injecting the `BulletTooltip` module into the services.

{% tab template="bullet-chart/getting-started/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletTooltip} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='tooltip'
                        style={{ textAlign: "center" }}
                        animation={{ enable: false }}
                        tooltip={{ enable: true }}
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={300}
                        interval={50}
                        dataSource={[{value: 270, target: 250}]}>
                        <Inject services={[BulletTooltip]}/>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}