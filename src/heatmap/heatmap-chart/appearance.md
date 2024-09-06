---
title: "Appearance"
component: "Heatmap"
description: "This section describes on how to customize the overall apperance of the Heatmap, like adding borders for heatmap cells or data points, adding margin and title for heatmap layout, mouse hover highligting options for the cells and formatting options for the data labels"
---

# Appearance

## Cell/customizations

You can customize the cell by using the [`cellSettings`](../api/heatmap/#cellsettings) property.

## Border

Change the width, color, and radius of the heat map cells by using the [`border`](../api/heatmap/cellSettings/#border) property.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
                border: {
                    width: 1,
                    radius: 4,
                    color: 'white'
                }
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Cell highlighting

Enable or disable the cell highlighting while hover over the heat map cells by using the  [`enableCellHighlighting`](../api/heatmap/cellSettings/#enablecellhighlighting) property.

>Note: The cell highlighting only works in a SVG rendering mode.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
               enableCellHighlighting: true
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Color gradient mode

You can set the minimum and maximum value colors based on row and column using the `colorGradientMode` property.
The types of colorGradientMode,

* Table: The minimum and maximum value colors calculated for overall data.
* Row: The minimum and maximum value colors calculated for each row of data.
* Column: The minimum and maximum value colors calculated for each column of data.

>Note: The default value of `colorGradientMode` is Table.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            paletteSettings = {{
                colorGradientMode: 'Column'
            }}
            cellSettings = { {
               enableCellHighlighting: true
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Margin

Set the margin for the heat map from its container by using the  [`margin`](../api/heatmap/#margin) property.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
    render() {
    return ( <HeatMapComponent id='heatmap'
            margin = { {
                left: 15,
                right: 15,
                top: 15,
                bottom: 15
             } }
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Title

The title is used to provide a quick information about the data plotted in heat map. The [`text`](../api/heatmap/title/#text) property is used to set the title for heat map. You can also customize text style of a title by using the [`textStyle`](../api/heatmap/title/#textstyle) property.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
    render() {
    return ( <HeatMapComponent id='heatmap'
            titleSettings = { {
                text: 'Sales Revenue per Employee (in 1000 US$)',
                textStyle: {
                    size: '15px',
                    fontWeight: '500',
                    fontStyle: 'Italic',
                    fontFamily: 'Segoe UI'
                }
            } }
            xAxis = { {
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip, Legend]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Data label

You can toggle the visibility of data labels by using the [`showLabel`](../api/heatmap/cellSettings/#showlabel) property. By default, the data label will be visible.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
               showLabel: false
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Text style

You can customize the font family, font size, and color of the data label by using the [`textStyle`](../api/heatmap/cellSettings/#textstyle) in the [`cellSettings`](../api/heatmap/#cellsettings) property.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
                textStyle: {
                    fontStyle: 'Italic',
                    fontFamily: 'Segoe UI'
                }
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Format

You can change the format of the data label, such as currency, decimal, percent etc. by using [`format`](../api/heatmap/cellSettings/#format) property.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

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
            [74, 33, 88, 23, 86, 59]
    ];
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
                labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            } }
            yAxis = { {
                labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
            } }
            cellSettings = { {
               format: '{value} $'
            } }
            dataSource={this.heatmapData}>
            <Inject services={[Tooltip]} />
            </HeatMapComponent> );
    }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## Customize the cell value

In the HeatMap, you can customize the cell value using the [`cellRender`](../api/heatmap/#cellrender) client-side event.

{% tab template= "heatmap/appearance", sourceFiles="app/**/*.tsx", compileJsx=true%}

```typescript

import * as React from "react";
import * as ReactDOM from 'react-dom';
import { HeatMapComponent, Inject, Legend, Tooltip, Adaptor } from '@syncfusion/ej2-react-heatmap';

class App extends React.Component {
      heatmapData: any[] = [
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
    [74, 33, 88, 23, 86, 59]
  ];

  render() {
    return (
      <HeatMapComponent
        id="heatmap"
        titleSettings={{
          text: 'Sales Revenue per Employee (in 1000 US$)',
          textStyle: {
            size: '15px',
            fontWeight: '500',
            fontStyle: 'Normal',
            fontFamily: 'Segoe UI'
          }
        }}
        xAxis={{
          labels: [
            'Nancy',
            'Andrew',
            'Janet',
            'Margaret',
            'Steven',
            'Michael',
            'Robert',
            'Laura',
            'Anne',
            'Paul',
            'Karin',
            'Mario'
          ]
        }}
        yAxis={{
          labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat']
        }}
        cellRender={this.cellRender as any}
        dataSource={this.heatmapData}
      >
        <Inject services={[Tooltip]} />
      </HeatMapComponent>
    );
  }

  cellRender(args: ICellEventArgs): void {
    args.displayText = args.value + '$ ';
  }
}
ReactDOM.render(<App />, document.getElementById('heatmap'));

```

{% endtab %}

## See Also

* [To customize the appearance of tool tip](./tooltip/#customize-the-appearance-of-tooltip)