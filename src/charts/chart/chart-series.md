---
title: " Chart Series | React "

component: "Chart"

description: "Chart supports to render collection of series like multiple series or combination series."
---

# Chart Series

## Multiple Series

You can add multiple series to the chart by using [`series`](../api/chart/seriesModel/) property.
The series are rendered in the order as it is added to the series array.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Combination Series

Combination of different types like Line, column etc, can be rendered in a chart.

{% tab template="chart/series/combination", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, LineSeries, StackingColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: '2005', y: 1.2, y1: 0.5, y2: 0.7, y3: -0.8, y4: 1.5 },
    { x: '2006', y: 1, y1: 0.5, y2: 1.4, y3: 0, y4: 2.3 },
    { x: '2007', y: 1, y1: 0.5, y2: 1.5, y3: -1, y4: 2 },
    { x: '2008', y: 0.25, y1: 0.35, y2: 0.35, y3: -.35, y4: 0.1 },
    { x: '2009', y: 0.1, y1: 0.9, y2: -2.7, y3: -0.3, y4: -2.7 },
    { x: '2010', y: 1, y1: 0.5, y2: 0.5, y3: -0.5, y4: 1.8 },
    { x: '2011', y: 0.1, y1: 0.25, y2: 0.25, y3: 0, y4: 2 },
    { x: '2012', y: -0.25, y1: -0.5, y2: -0.1, y3: -0.4, y4: 0.4 },
    { x: '2013', y: 0.25, y1: 0.5, y2: -0.3, y3: 0, y4: 0.9 },
    { x: '2014', y: 0.6, y1: 0.6, y2: -0.6, y3: -0.6, y4: 0.4 },
    { x: '2015', y: 0.9, y1: 0.5, y2: 0, y3: -0.3, y4: 1.3 }
  ];
  public primaryxAxis: AxisModel = { title: 'Years', interval: 1, labelIntersectAction: 'Rotate45', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'Growth', minimum: -3, maximum: 3, interval: 1 };
  public marker = { visible: true, width: 10, opacity: 0.6, height: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Annual Growth GDP in France'>
      <Inject services={[StackingColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Private Consumption'
          type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Government Consumption'
          type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y2' name='Investment'
          type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y3' name='Net Foreign Trade'
          type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y4' name='GDP' type='Line' opacity={0.6}
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};

ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: Bar series cannot be combined with any other series as the axis orientation is different from other series.