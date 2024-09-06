---
title: "Chart Data Editing | React"
component: "Chart"
description: "React Data Editing is one of the user interaction feature. It provides the chart data that to change their value by using mouse cursor"
---

<!-- markdownlint-disable MD036 -->

# Data Editing

## Enable Data Editing

We can use the data editing through inject the `DataEditing` module in the chart. It provides drag and drop support to the rendered points. Now, we can change the location or value of the point based on its `y` value.  To enable the data editing, set the `enable` property to true in the drag settings of the series. Also, we can set color using `fill` property and set the data editing minimum and maximum range using `minY` and `maxY` properties.

{% tab template="chart/user-interaction/data-editing", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, LineSeries, DataEditing}
from'@syncfusion/ej2-react-charts';

export let columnData: any[] = [
                { x: '2005', y: 21 }, { x: '2006', y: 60 },
                { x: '2007', y: 45 }, { x: '2008', y: 50 },
                { x: '2009', y: 74 }, { x: '2010', y: 65 },
                { x: '2011', y: 85 }
        ];
export let lineData: any[] = [
                { x: '2005', y: 21 }, { x: '2006', y: 22 },
                { x: '2007', y: 36 }, { x: '2008', y: 34 },
                { x: '2009', y: 54 }, { x: '2010', y: 55 },
                { x: '2011', y: 60 }
        ];
ReactDOM.render(
 <ChartComponent id='chart'
           primaryXAxis={ {  valueType: 'Category',
            minimum: -0.5,
            maximum: 6.5,
            labelPlacement: 'OnTicks',
            majorGridLines: { width: 0 } } }
            chartArea={{
            border: {
                width: 0
            }
            }}
           primaryYAxis={ { rangePadding: 'None',
            minimum: 0,
            title : 'Sales',
            labelFormat: '{value}%',
            maximum: 100,
            interval: 20,
            lineStyle: { width: 0 },
            majorTickLines: { width: 0 },
            minorTickLines: { width: 0 } } }
           title='Sales Prediction of Products'
           tooltip={{enable: true}}>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, LineSeries, DataEditing ]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={columnData}  xName='x' yName='y' name='Product A' type='Column' dragSettings={{enable: true}} marker={{visible: true, width: 10, height: 10}}>  </SeriesDirective>
        <SeriesDirective dataSource ={lineData}  xName='x' yName='y' name='Product B' type='Line' marker={{visible: true, width: 10, height: 10}} dragSettings={{enable: true}}> </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}
