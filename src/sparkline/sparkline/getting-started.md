# Getting Started

This section explains you the steps required to create a sparkline and demonstrate its basic usage.

## Dependencies

The following list of minimum dependencies are required to use the sparkline:

```tsx
|-- @syncfusion/ej2-react-charts
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-charts
    |-- @syncfusion/ej2-svg-base
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-pdf-export
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-compression
```

## Installation and Configuration

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

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-react-charts --save
```

## Add Sparkline to the Project

Now, you can start adding Sparkline component in the application. For getting started, add the Sparkline component in `src/index.tsx` file using following code.

{% tab compileJsx=true%}

```tsx

import * as React from 'react';
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
render() {
  return ( <SparklineComponent></SparklineComponent> );
 }
}
export default App;

```

{% endtab %}

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```

Since the data source has not been specified to the sparkline, no shape will be rendered. Only an empty SVG element is appended to the sparkline container.

## Module Injection

The sparkline component is segregated into individual feature-wise modules. To use a particular feature, inject its feature module using the `<Inject services={} />` method. The module available in sparkline and its descriptions is as follows.

* SparklineTooltip - Inject this provider to use tooltip series.

In the current application, the above basic sparkline is modified to visualize the types of sparkline.

In this application, tooltip feature of the sparkline is used. Now, import the SparklineTooltip module from the sparkline package, and inject it into the sparkline control using the `Sparkline.Inject` method.

{% tab compileJsx=true%}

```tsx

import * as React from 'react';
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
render() {
  return ( <SparklineComponent><Inject services={[SparklineTooltip]} /></SparklineComponent> );
 }
}
export default App;

```

{% endtab %}

## Bind data source to Sparkline

The dataSource property is used for binding data source to the sparkline. This property takes the collection value as input. For example, the list of objects can be provided as input.

{% tab template= "sparkline/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='100px' width='70%'
    dataSource={[
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ]}
    xName='xval' yName='yval'>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));

```

{% endtab %}

## Change the type of Sparkline

You can change the sparkline type by setting the [`type`] property to [`Line`], [`Column`], [`WinLoss`], [`Pie`], or [`Area`]. Here, the sparkline type has been set to [`area`].

{% tab template= "sparkline/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='100px' width='70%'
    dataSource={[
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ]}
    xName='xval' yName='yval' type='Area'>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));

```

{% endtab %}

## Enable tooltip for Sparkline

The sparkline displays additional information through tooltip when the mouse is hovered over the sparkline. You can enable tooltip by setting the [`visible`] property to true in [`tooltipSettings`] and injecting `SparklineTooltip` module using the `Sparkline.Inject(SparklineTooltip )` method.

{% tab template= "sparkline/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='100px' width='70%'
    tooltipSettings={ {
        visible: true, format: '${xval} : ${yval}',
    } }
    dataSource={[
        { x: 0, xval: '2005', yval: 20090440 },
        { x: 1, xval: '2006', yval: 20264080 },
        { x: 2, xval: '2007', yval: 20434180 },
        { x: 3, xval: '2008', yval: 21007310 },
        { x: 4, xval: '2009', yval: 21262640 },
        { x: 5, xval: '2010', yval: 21515750 },
        { x: 6, xval: '2011', yval: 21766710 },
        { x: 7, xval: '2012', yval: 22015580 },
        { x: 8, xval: '2013', yval: 22262500 },
        { x: 9, xval: '2014', yval: 22507620 },
    ]}
    xName='xval' yName='yval' type='Area'>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));

```

{% endtab %}