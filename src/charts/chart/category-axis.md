---
title: " Chart Category Axis | React "

component: "Chart"

description: "Category axis are used to represent, the string values instead of numbers.It contains range, label placement customizations."
---

# Category Axis

Category axis are used to represent, the string values instead of numbers.

To get start quickly with React Category Axis, you can check out this video:

`youtube:PS4WWiu4TYM`

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: To use category axis, we need to inject `Category` module into the `services` and
set the [`valueType`](../api/chart/axisModel/#valuetype) of axis to Category.

## Labels Placement

By default, category labels are placed between the ticks in an axis, this can also be placed on ticks
using [`labelPlacement`](../api/chart/axisModel/#labelplacement) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries', labelPlacement: 'OnTicks' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}
      title='Olympic Medals'  >
      <Inject services={[ColumnSeries, Legend, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Range

Range of the category axis can be customized using [`minimum`](../api/chart/axisModel/#minimum),
[`maximum`](../api/chart/axisModel/#maximum) and [`interval`](../api/chart/axisModel/#interval) property of
the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries', interval: 2, minimum: 1, maximum: 5 };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}
      title='Olympic Medals'  >
      <Inject services={[ColumnSeries, Legend, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Indexed category axis

Category axis also can be rendered based on the index values of data source. This can be achieved by defining
the `isIndexed` property to `true` in the axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent,ColumnSeries,Inject,Legend,
  SeriesCollectionDirective, SeriesDirective }from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public  data1: any[] = [{ x: 'Myanmar', y: 7.3 }, { x: 'India', y: 7.9 },
                           { x: 'Bangladesh', y: 6.8 }, { x: 'Cambodia', y: 7.0 }, { x: 'China', y: 6.9 }];
    public  data2: any[] = [{ x: 'Poland', y: 2.7 },{ x: 'Australia', y: 2.5 },
                           { x: 'Singapore', y: 2.0 },{ x: 'Canada', y: 1.4 },{ x: 'Germany', y: 1.8 }];
    public primaryxAxis: AxisModel= { valueType: 'Category',   isIndexed: true } ;

    render() {
            return <ChartComponent id='charts'
                    primaryXAxis={ this.primaryxAxis }>
                        <Inject services={[ColumnSeries, Legend, Category]}/>
                        <SeriesCollectionDirective>
                            <SeriesDirective dataSource ={this.data1}  xName='x' yName='y' type='Column'/>
                            <SeriesDirective dataSource ={this.data1}  xName='x' yName='y' type='Column'/>
                        </SeriesCollectionDirective>
                  </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}