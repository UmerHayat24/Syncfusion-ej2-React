---
title: " Chart Working With Data | React "

component: "Chart"

description: "Chart can be rendered by using different types of data source. They are called local data, remote data and empty points. "
---

<!-- markdownlint-disable MD036 -->

# Working with Data

Chart can visualise data bound from local or remote data.

## Local Data

You can bind a simple JSON data to the chart using [`dataSource`](../api/chart/seriesModel/#datasource)
property in series. Now map the fields in JSON to [`xName`](../api/chart/seriesModel/#xname) and
[`yName`](../api/chart/seriesModel/#yname) properties.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, Inject, Legend, LineSeries,
SeriesCollectionDirective, SeriesDirective  } from '@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' type='Column' yName='sales' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Lazy loading

Lazy loading allows you to load data for chart on demand. Chart will fire the scrollEnd event, in that we can
get the minimum and maximum range of the axis, based on this, we can upload the data to chart.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {  ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
    ChartTheme, ScrollBar, Zoom, IScrollEventArgs, LineSeries, Tooltip,
    DateTime, ILoadedEventArgs, Chart, Crosshair, ColumnSeries  } from '@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

 private chart: ChartComponent;
 private intl: Internationalization = new Internationalization();

     private GetDateTimeData(start: Date, end: Date): { x: Date, y: number }[] {
        let series1: { x: Date, y: number }[] = [];
        let date: number;
        let value: number = 30;
        let option: DateFormatOptions = {
            skeleton: 'full',
            type: 'dateTime'
        };
        let dateParser: Function = this.intl.getDateParser(option);
        let dateFormatter: Function = this.intl.getDateFormat(option);
        for (let i: number = 0; start <= end; i++) {
            date = Date.parse(dateParser(dateFormatter(start)));
            if (Math.random() > .5) {
                value += (Math.random() * 10 - 5);
            } else {
                value -= (Math.random() * 10 - 5);
            }
            if (value < 0) {
                value = this.getRandomInt(20, 40);
            }
            let point1: { x: Date, y: number } = { x: new Date(date), y: Math.round(value) };
            new Date(start.setDate(start.getDate() + 1));
            series1.push(point1);
        }
        return series1;
    }

   private getRandomInt(min: number, max: number): number {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
  render() {
    return   <ChartComponent id='charts'
                           ref={chart => this.chart = chart}
                            primaryXAxis={{
                                title: 'Day',
                                valueType: 'DateTime',
                                edgeLabelPlacement: 'Shift',
                                skeleton: 'yMMM',
                                skeletonType: 'Date',
                                scrollbarSettings: {
                                    range: {
                                        minimum: new Date(2009, 0, 1),
                                        maximum: new Date(2014, 0, 1)
                                    },
                                    enable: true,
                                }
                            }}
                            primaryYAxis={{
                                title: 'Server Load',
                                labelFormat: '{value}MB'
                            }}
                            crosshair={{ enable: true, lineType: 'Vertical' }}
                            chartArea={{ border: { width: 0 } }}
                            tooltip={{ enable: true }}
                            legendSettings={{ visible: true }}
                           // scrollStart={this.scrollStart.bind(this)}
                            scrollEnd={this.scrollEnd.bind(this)}
                            title='Network Load' height='450' width='100%' >
                            <Inject services={[LineSeries, DateTime, Tooltip, ScrollBar, Zoom, Crosshair]} />
                            <SeriesCollectionDirective>
                                <SeriesDirective dataSource={this.GetDateTimeData(new Date(2009, 0, 1), new Date(2009, 8, 1))} xName='x' yName='y'
                                    type='Line' animation={{ enable: false }}>
                                </SeriesDirective>
                            </SeriesCollectionDirective>
                        </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Common Datasource

You can also bind a JSON data common to all series using  [`dataSource`](../api/chart/seriesModel/#datasource) property in chart.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, Inject, Legend, LineSeries,
SeriesCollectionDirective, SeriesDirective  } from '@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [
      { month: 'Jan', sales: 35, sales1: 28 }, { month: 'Feb', sales: 28, sales1: 35 },
      { month: 'Mar', sales: 34, sales1: 32 }, { month: 'Apr', sales: 32, sales1: 34 },
      { month: 'May', sales: 40, sales1: 32 }, { month: 'Jun', sales: 32, sales1: 40 },
      { month: 'Jul', sales: 35, sales1: 55 }, { month: 'Aug', sales: 55, sales1: 35 },
      { month: 'Sep', sales: 38, sales1: 30 }, { month: 'Oct', sales: 30, sales1: 38 },
      { month: 'Nov', sales: 25, sales1: 32 }, { month: 'Dec', sales: 32, sales1: 25 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis} dataSource={this.chartData}>
      <Inject services={[ColumnSeries, Legend, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective  xName='month' type='Column' yName='sales'  />
        <SeriesDirective  xName='month' type='Column' yName='sales1' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Remote Data

You can also bind remote data to the chart using `DataManager`. The DataManager requires minimal information
like webservice URL, adaptor and crossDomain to interact with service endpoint properly. Assign the instance
 of DataManager to the [`dataSource`](../api/chart/seriesModel/#datasource) property in series and map
 the fields of data to [`xName`](../api/chart/seriesModel/#xname) and
[`yName`](../api/chart/seriesModel/#yname) properties. You can also use the
[`query`](../api/chart/seriesModel/#query) property of the series to filter the data.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { DataManager,Query} from '@syncfusion/ej2-data'
import { AxisModel,Category,ChartComponent, ColumnSeries, Inject, Legend, LineSeries, SeriesCollectionDirective, SeriesDirective  } from '@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public dataManager = new DataManager({
    url: 'http://mvc.syncfusion.com/Services/Northwnd.svc/Tasks/'
  });
  public query = new Query().take(5).where('Estimate', 'lessThan', 3, false);
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Asignee' };
  public primaryyAxis: AxisModel = { title: 'Estimate', minimum: 0, maximum: 3, interval: 1 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries, Legend, Category, LineSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.dataManager} xName='Assignee' type='Column' yName='Estimate' name='Sales' query={this.query} />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Empty points

The Data points that uses the `null` or `undefined` as value are considered as empty points. Empty data points are ignored and
not plotted in the Chart. When the data is provided by using the points property,
By using `emptyPointSettings` property in series, you can customize the empty point. Default `mode` of the empty point is `Gap`.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, Inject, LineSeries,
SeriesCollectionDirective, SeriesDirective  } from '@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: null },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: undefined },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, LineSeries, ColumnSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' type='Column' yName='sales' name='Sales' />
        <SeriesDirective dataSource={this.data} xName='month' type='Line' yName='sales' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Empty point color**

Specific color for empty point can be set by `fill` property in `emptyPointSettings`.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, EmptyPointSettingsModel,
Inject, LineSeries, SeriesCollectionDirective, SeriesDirective  } from '@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: null },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: undefined },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public emptyPointSettings1: EmptyPointSettingsModel = { mode: 'Average', fill: 'pink' };
  public emptyPointSettings2: EmptyPointSettingsModel = { mode: 'Zero', fill: 'green' };

  render() {
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, LineSeries, ColumnSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' type='Column' yName='sales' name='Sales' emptyPointSettings={this.emptyPointSettings1} />
        <SeriesDirective dataSource={this.data} xName='month' type='Line' yName='sales' name='Sales' emptyPointSettings={this.emptyPointSettings2} />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}
