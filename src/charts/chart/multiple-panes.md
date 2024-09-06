---
title: " Chart Multiple-panes | React "

component: "Chart"

description: "Chart can be divided multiple rows and columns. Axes are rendering based on row index or column index in pane."
---

# Multiple Panes

Chart area can be divided into multiple panes using [`rows`](../api/chart/rowModel/) and [`columns`](../../api/chart/columnModel/).

## Rows

To split the chart area vertically into number of rows, use [`rows`](../api/chart/rowModel/) property of the chart.

*1. You can allocate space for each row by using the [`height`](../api/chart/rowModel/#height) property.
  The value can be either in percentage or in pixel.*

*2. To associate a vertical axis to a particular row, specify its index to
  [`rowIndex`](../api/chart/axisModel/#rowindex) property of the axis.*

*3. To customize each row’s bottom line, use [`border`](../api/chart/rowModel/#border) property.*

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, RowsDirective, RowDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
    { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
    { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
    { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Months', interval: 1 };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)', minimum: 0, maximum: 90, interval: 20,
    lineStyle: { width: 0 }, labelFormat: '{value}°F'
  };
  public lines = { width: 0 };
  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Weather Condition'>
      <Inject services={[ColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <AxesDirective>
        <AxisDirective rowIndex={1} name='yAxis1' opposedPosition={true} title='Temperature (Celsius)'
          labelFormat='{value}°C' minimum={24} maximum={36} interval={2}
          majorGridLines={this.lines} lineStyle={this.lines} >
        </AxisDirective>
      </AxesDirective>
      <RowsDirective>
        <RowDirective height='50%' ></RowDirective>
        <RowDirective height='50%' ></RowDirective>
      </RowsDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Germany' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Japan' type='Line'
          marker={this.marker} yAxisName='yAxis1' >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

For spanning the vertical axis along multiple row, you can use [`span`](../api/chart/axisModel/#span) property of an axis.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
    { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
    { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
    { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Months', interval: 1 };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)', minimum: 0, maximum: 90, interval: 20,
    lineStyle: { width: 0 }, labelFormat: '{value}°F'
  };
  public lines = { width: 0 };
  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Weather Condition'>
      <Inject services={[ColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <AxesDirective>
        <AxisDirective rowIndex={1} name='yAxis1' opposedPosition={true} title='Temperature (Celsius)'
          labelFormat='{value}°C' minimum={24} maximum={36} interval={2}
          majorGridLines={this.lines} lineStyle={this.lines} >
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Germany' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Japan' type='Line'
          marker={this.marker} yAxisName='yAxis1' >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Columns

To split the chart area horizontally into number of columns, use [`columns`](../api/chart/columnModel/) property of the chart.

*1. You can allocate space for each column by using the [`width`](../api/chart/columnModel/#width)
property. The given width can be either in percentage or in pixel.*

*2. To associate a horizontal axis to a particular column, specify its index to
  [`columnIndex`](../api/chart/axisModel/#columnindex) property of the axis.*

*3. To customize each column’s bottom line, use [`border`](../api/chart/columnModel/#border)
  property.*

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, ColumnsDirective, ColumnDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
    { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
    { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
    { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Months', interval: 1 };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)', minimum: 0, maximum: 90, interval: 20,
    lineStyle: { width: 0 }, labelFormat: '{value}°F'
  };
  public lines = { width: 0 };
  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Weather Condition'>
      <Inject services={[ColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <AxesDirective>
        <AxisDirective columnIndex={1} name='xAxis1' opposedPosition={true} valueType='Category'
          majorGridLines={this.lines} lineStyle={this.lines} >
        </AxisDirective>
      </AxesDirective>
      <ColumnsDirective>
        <ColumnDirective width='50%' ></ColumnDirective>
        <ColumnDirective width='50%' ></ColumnDirective>
      </ColumnsDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Germany' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Japan' type='Line'
          marker={this.marker} xAxisName='xAxis1' >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

For spanning the horizontal axis along multiple column, you can use [`span`](../api/chart/axisModel/#span) property of an axis.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, ColumnsDirective, ColumnDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
    { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
    { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
    { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', span: 2, title: 'Months', interval: 1 };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)', minimum: 0, maximum: 90, interval: 20,
    lineStyle: { width: 0 }, labelFormat: '{value}°F'
  };
  public lines = { width: 0 };
  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Weather Condition'>
      <Inject services={[ColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <AxesDirective>
        <AxisDirective columnIndex={1} name='xAxis1' opposedPosition={true} valueType='Category'
          majorGridLines={this.lines} lineStyle={this.lines} >
        </AxisDirective>
      </AxesDirective>
      <ColumnsDirective>
        <ColumnDirective width='50%' ></ColumnDirective>
        <ColumnDirective width='50%' ></ColumnDirective>
      </ColumnsDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Germany' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Japan' type='Line'
          marker={this.marker} xAxisName='xAxis1' >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}