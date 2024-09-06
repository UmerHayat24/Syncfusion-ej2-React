---
title: " Chart Axis | Vue "

component: "Chart"

description: "Chart Axis represents the two major axis namely primary x axis and primary y axis."
---

# Axis

Chart typically has two axis, which are used to measure and categorize data:
a horizontal or primary x axis and a vertical or primary y axis.

Vertical axis supports numerical and logarithmic scale. Horizontal axis supports
the following types of scale.

* Category
* Numeric
* DateTime
* Logarithmic

In addition to this, both vertical and horizontal axis support inversed axis.

<!-- markdownlint-disable MD036 -->
**Positioning Axis Labels**
<!-- markdownlint-disable MD036 -->

By default, category labels are placed between the ticks in an axis, this can also be placed on ticks
using [`labelPlacement`](../api/chart/axisModel/#labelplacement) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
             { country: "USA", gold: 50, silver: 70, bronze: 45 },
             { country: "China", gold: 40, silver: 60, bronze: 55 },
             { country: "Japan", gold: 70, silver: 60, bronze: 50 },
             { country: "Australia", gold: 60, silver: 56, bronze: 40 },
             { country: "France", gold: 50, silver: 45, bronze: 35 },
             { country: "Germany", gold: 40, silver: 30, bronze: 22 },
             { country: "Italy", gold: 40, silver: 35, bronze: 37 },
             { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
ReactDOM.render(
 <ChartComponent id='charts' primaryXAxis={ { valueType: 'Category', title:'Countries',
           labelPlacement: 'OnTicks'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);
```

{% endtab %}

>Note: To use category axis, we need to inject `Category` module into the `services` and
set the [`valueType`](../api/chart/axisModel/#valuetype) of axis to `Category`.

<!-- markdownlint-disable MD013 -->

## Label Format

**Numeric Label Format**

Numeric labels can be formatted by using the [`labelFormat`](../api/chart/axisModel/#labelformat) property. Numeric labels supports all globalize format.

{% tab template="chart/axis/double", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Logarithmic, Tooltip, DataLabel, Zoom, Crosshair, AreaSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { x: 1900, y: 4, y1: 2.6, y2: 2.8 }, { x: 1920, y: 3.0, y1: 2.8, y2: 2.5 },
                { x: 1940, y: 3.8, y1: 2.6, y2: 2.8 }, { x: 1960, y: 3.4, y1: 3, y2: 3.2 },
                { x: 1980, y: 3.2, y1: 3.6, y2: 2.9 }, { x: 2000, y: 3.9, y1: 3, y2: 2 }
        ];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ { edgeLabelPlacement: 'Shift', title:'Years'} }
           primaryYAxis={ { labelFormat: 'c',title:'Sales Amount in Millions'} }
           title='Average Sales Comparison'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, AreaSeries]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='Product X' type='Area'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Product Y' type='Area'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y2' name='Product Z' type='Area'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

The following table describes the result of applying some commonly used label formats on numeric values.

<!-- markdownlint-disable MD033 -->

<table>
<tr>
<td><b>Label Value</b></td>
<td><b>Label Format property value</b></td>
<td><b>Result </b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>1000</td>
<td>n1</td>
<td>1000.0</td>
<td>The Number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n2</td>
<td>1000.00</td>
<td>The Number is rounded to 2 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n3</td>
<td>1000.000</td>
<td>The Number is rounded to 3 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p1</td>
<td>1.0%</td>
<td>The Number is converted to percentage with 1 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p2</td>
<td>1.00%</td>
<td>The Number is converted to percentage with 2 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p3</td>
<td>1.000%</td>
<td>The Number is converted to percentage with 3 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c1</td>
<td>$1,000.0</td>
<td>The Currency symbol is appended to number and number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c2</td>
<td>$1,000.00</td>
<td>The Currency symbol is appended to number and number is rounded to 2 decimal place</td>
</tr>
</table>

**Datetime Label Format**

You can format and parse the date to all globalize format using [`labelFormat`](../api/chart/axisModel/#labelformat) property in an axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Logarithmic, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { x: new Date(2000, 6, 11), y: 10 }, { x: new Date(2002, 3, 7), y: 30 },
                { x: new Date(2004, 3, 6), y: 15 }, { x: new Date(2006, 3, 30), y: 65 },
                { x: new Date(2008, 3, 8), y: 90 }, { x: new Date(2010, 3, 8), y: 85 }
        ];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'DateTime', title:'Sales Across Years', labelFormat: 'yMd'} }
           primaryYAxis={ { title:'Sales Amount in millions(USD)'} }
           title='Average Sales Comparison'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

The following table describes the result of applying some common date time formats to the labelFormat property

<!-- markdownlint-disable MD033 -->

<table>
<tr>
<td><b>Label Value</b></td>
<td><b>Label Format Property Value</b></td>
<td><b>Result </b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>EEEE</td>
<td>Monday</td>
<td>The Date is displayed in day format</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>yMd</td>
<td>04/10/2000</td>
<td>The Date is displayed in month/date/year format</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td> MMM </td>
<td>Apr</td>
<td>The Shorthand month for the date is displayed</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>hm</td>
<td>12:00 AM</td>
<td>Time of the date value is displayed as label</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>hms</td>
<td>12:00:00 AM</td>
<td>The Label is displayed in hours:minutes:seconds format</td>
</tr>
</table>

<!-- markdownlint-disable MD033 -->

**Custom Label Format**

Axis also supports custom label format using placeholder like {value}°C, in which the value represents the axis label. e.g 20°C.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Logarithmic, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category', title:'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20,labelFormat:'${value}K',title:'Medals'} }
           title='Olympic Medals'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

## Inversed Axis

When an axis is inversed, highest value of the axis comes closer to origin and vice versa. To place an axis in inversed manner set this property
 [`isInversed`](../api/chart/axisModel/#isinversed) to true.

 {% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

 ```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, DataLabel}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
    { x: 2008, y: 15.1 }, { x: 2009, y: 16 }, { x: 2010, y: 21.4 },
    { x: 2011, y: 18 }, { x: 2012, y: 16.2 }, { x: 2013, y: 11 },
    { x: 2014, y: 7.6 }, { x: 2015, y: 1.5 }
];

ReactDOM.render(
    <ChartComponent id='charts'
            primaryXAxis={ { valueType: 'Category', title: 'Years', opposedPosition: true,  isInversed: true } }
            primaryYAxis={ { title: 'Exchange rate (INR per USD)', edgeLabelPlacement: 'Shift', labelIntersectAction: 'Rotate45',
                            isInversed: true } }
            title='Exchange Rate'>
            <Inject services={[ColumnSeries, Category, Legend, DataLabel]} />
            <SeriesCollectionDirective>
            <SeriesDirective dataSource={data} xName='x' yName='y' type='Column' marker={ {dataLabel:{visible: true} } }>
            </SeriesDirective>
            </SeriesCollectionDirective>
            </ChartComponent>, document.getElementById('charts')

);

```

{% endtab %}

## Common Axis Features

**Axis Title**

You can add a title to the axis using [`title`](../api/chart/axisModel/#title) property to provide quick information to the user about the data plotted in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Logarithmic, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category', title:'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20,labelFormat: '${value}K',
           title:'Medals', titleStyle: {
            size: '16px', color: 'grey',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           } } }
           title='Olympic Medals'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Label Customization**

The [`labelStyle`](../api/chart/axisModel/#labelstyle) property of an axis provides options to customize the `color`, `font-family`, `font-size` and `font-weight` of the axis labels.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Logarithmic, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category', title:'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20,labelFormat: '${value}K',
           title:'Medals', titleStyle: {
            size: '16px', color: 'grey',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           },labelStyle: {
            size: '14px', color: 'blue',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           } } }
           title='Olympic Medals'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}