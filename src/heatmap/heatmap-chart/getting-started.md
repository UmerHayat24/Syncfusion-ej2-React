---
title: "Getting started"
component: "Heatmap"
description: "This section describes on how to visualize a two-dimensional data by enabling the basic features in heatmap"
---

# Getting Started

This section explains the steps required to create a heat map and demonstrates the basic usage of the heat map control.

## Dependencies

For using heat map, the following minimum requirements are needed.

```typescript
|-- @syncfusion/ej2-react-heatmap
    |-- @syncfusion/ej2-heatmap
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-svg-base
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
npm install @syncfusion/ej2-react-heatmap --save
```

## Adding heat map to the project

Now, you can start adding HeatMap component in the application. For getting started, add the HeatMap component in `src/App.tsx` file using following code.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import { HeatMapComponent } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
render() {
  return ( <HeatMapComponent></HeatMapComponent> );
 }
}
export default App;

```

{% endtab %}

Use the `npm start` command to run the application in the browser.

```sh
npm start
```

The below example shows a basic HeatMap.

{% tab template="heatmap/getting-started", sourceFiles="app/**/*.tsx",  isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { HeatMapComponent} from '@syncfusion/ej2-react-heatmap';
ReactDOM.render(<HeatMapComponent id='heatmap'></HeatMapComponent>, document.getElementById('heatmap'));

```

{% endtab %}

## Module injection

The heat map components are segregated into individual feature-wise modules. To use its feature, you need to inject its feature service in the AppModule. In the current application,the basic heat map is modified to visualize sales revenue data for week, and  the tooltip and legend features of the heat map are used. Find the relevant feature modules and descriptions as follows.

* Legend - Provides the legend feature by injecting it.
* Tooltip - Provides the tooltip feature by injecting it.

Now, import the above-mentioned modules from the heat map package and inject them into `services`.

 ```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { HeatMapComponent, Inject, Legend, Tooltip} from '@syncfusion/ej2-react-heatmap';

ReactDOM.render(<HeatMapComponent id='heatmap'></HeatMapComponent>,
 <Inject services={[Legend, Tooltip]}/>
document.getElementById('heatmap'));

 ```

## Populate heat map with data

This section explains how to populate the following two-dimensional array data to the heat map.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```typescript

import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';
import * as ReactDOM from "react-dom";
import * as React from "react";

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    public render() {
    return ( <HeatMapComponent id='heatmap'
            dataSource={this.heatmapData}>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Enable axis labels

You can add axis labels to the heat map and format those labels using the [`xAxis`](../api/heatmap/#xaxis) and [`yAxis`](../api/heatmap/#yaxis) properties. Axis labels provide additional information about the data points populated in the heat map.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    render() {
    return ( <HeatMapComponent id='heatmap'
            xAxis = { {
                labels : ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
                'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
            } }
            yAxis = { {
                labels : ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Add heat map title

Add a title using the [`titleSettings`](../api/heatmap/#titlesettings) property to the heat map to provide quick information to the user about the data populated in the heat map.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    render() {
    return ( <HeatMapComponent id='heatmap'
            titleSettings = { {
                text: 'Sales Revenue per Employee (in 1000 US$)',
                textStyle: {
                    size: '15px',
                    fontWeight: '500',
                    fontStyle: 'Normal',
                    fontFamily: 'Segoe UI'
                }
            } }
            xAxis = { {
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
                'Laura', 'Anne', 'Paul', 'Karin', 'Mario']
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Enable legend

Use a legend for the heat map in the [`legendSettings`](../api/heatmap/#legendsettings) object by setting the [`visible`](../api/heatmap/legendSettings/#visible) property to true and injecting the `Legend` module into the `services`.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx",compileJsx=true %}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    render() {
    return ( <HeatMapComponent id='heatmap'
            titleSettings = { {
                text: 'Sales Revenue per Employee (in 1000 US$)',
                textStyle: {
                    size: '15px',
                    fontWeight: '500',
                    fontStyle: 'Normal',
                    fontFamily: 'Segoe UI'
                }
            } }
            xAxis = { {
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
                'Laura', 'Anne', 'Paul', 'Karin', 'Mario']
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            dataSource={this.heatmapData}
            legendSettings = { {
                visible:true,
                position: 'Right',
                showLabel: true,
                height: "150"
            } }>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> )
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Add data label

Add data labels to improve the readability of the heat map. This can be achieved by setting the [`showLabel`](../api/heatmap/cellSettings/#showlabel) property to true in the [`cellSettings`](../api/heatmap/#cellsettings) object.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    render() {
    return ( <HeatMapComponent id='heatmap'
            titleSettings= { {
                text: 'Sales Revenue per Employee (in 1000 US$)',
                textStyle: {
                    size: '15px',
                    fontWeight: '500',
                    fontStyle: 'Normal',
                    fontFamily: 'Segoe UI'
                }
            } }
            xAxis = { {
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
                'Laura', 'Anne', 'Paul', 'Karin', 'Mario']
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
                showLabel: true,
            } }
            dataSource={this.heatmapData}
            legendSettings = { {
                position: 'Right',
                showLabel: true,
                height: "150"
            } }>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Add custom cell palette

The default palette settings of the heat map cells can be customized by using the [`paletteSettings`](../api/heatmap/#palettesettings) property.
Using the [`palette`](../api/heatmap/paletteSettings/#palette) property in `paletteSettings` object, you can change the color set for the cells. You can change the color mode of the cells to fixed or gradient mode using the [`type`](../api/heatmap/paletteSettings/#type) property.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript
import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    render() {
    return ( <HeatMapComponent id='heatmap'
            titleSettings = { {
                text: 'Sales Revenue per Employee (in 1000 US$)',
                textStyle: {
                    size: '15px',
                    fontWeight: '500',
                    fontStyle: 'Normal',
                    fontFamily: 'Segoe UI'
                }
            } }
            xAxis = { {
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
                'Laura', 'Anne', 'Paul', 'Karin', 'Mario']
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
                showLabel: true,
            } }
            paletteSettings = { {
                palette: [
                    { value: 0, color: '#C06C84' },
                    { value: 50, color: '#6C5B7B' },
                    { value: 100, color: '#355C7D' }
                ],
                type: "Gradient"
            } }
            dataSource={this.heatmapData}
            legendSettings = { {
                position: 'Right',
                showLabel: true,
                height: "150"
            } }>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Enable tooltip

The tooltip is used when you cannot display information by using the data labels due to space constraints. You can enable the tooltip by setting the [`showTooltip`](../api/heatmap/#showtooltip) property to `true` and injecting the `Tooltip` module into the `services`.

{% tab template= "heatmap/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
    private heatmapData: any [] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];
    render() {
    return ( <HeatMapComponent id='heatmap'
            titleSettings = { {
                text: 'Sales Revenue per Employee (in 1000 US$)',
                textStyle: {
                    size: '15px',
                    fontWeight: '500',
                    fontStyle: 'Normal',
                    fontFamily: 'Segoe UI'
                }
            } }
            xAxis = { {
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
                'Laura', 'Anne', 'Paul', 'Karin', 'Mario']
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
                showLabel: true,
            } }
            dataSource={this.heatmapData}
            showTooltip={true}
            legendSettings = { {
                visible:true,
                position: 'Right',
                showLabel: true,
                height: "150"
            } }>
            <Inject services={[Legend, Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}