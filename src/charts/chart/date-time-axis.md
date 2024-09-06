---
title: " Chart Datetime Axis | React "

component: "Chart"

description: "Date time axis uses date time scale and displays the date time values as axis labels in the specified format."
---
<!-- markdownlint-disable MD036 -->

# DateTime and DateTimeCategory Axis

## DateTime Axis

Date time axis uses date time scale and displays the date time values as axis labels in the specified format.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', title: 'Sales Across Years', labelFormat: 'yMMM' };
  public primaryyAxis: AxisModel = { title: 'Sales Amount in millions(USD)' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: To use datetime axis, we need to inject `DateTime` module into the `services` and
set the [`valueType`](../api/chart/axis/#valuetype) of axis to DateTime.

## DateTimeCategory Axis

Date-time category axis is used to display the date-time values with non-linear intervals.
For example, the business days alone have been depicted in a week here.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTimeCategory, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeCategoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTimeCategory', skeleton: 'Ed' };
  public primaryyAxis: AxisModel = { title: 'Sales Amount in millions(USD)' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTimeCategory]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeCategoryData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: To use dateTimeCategory axis, we need to inject `DateTimeCategory` module into the `services` method and
set the [`valueType`](../api/chart/axis/#valuetype) of axis to DateTimeCategory.

### Range

Range for an axis, will be calculated automatically based on the provided data, you can also customize
the range of the axis using [`minimum`](../api/chart/axis/#minimum),
[`maximum`](../api/chart/axis/#maximum) and [`interval`](../api/chart/axis/#interval) property of the
axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'DateTime', title: 'Sales Across Years', labelFormat: 'yMMM',
    minimum: new Date(2000, 6, 1), maximum: new Date(2010, 6, 1)
  };
  public primaryyAxis: AxisModel = { title: 'Sales Amount in millions(USD)' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Interval Customization

Date time intervals can be customized by using the [`interval`](../api/chart/axis/#interval)
and [`intervalType`](../api/chart/axis/#intervaltype) properties of the axis. For example, when you
set interval as 2 and intervalType as years, it considers 2 years as interval.

DateTime axis supports following interval types,

* Auto
* Years
* Months
* Days
* Hours
* Minutes
* Seconds

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', title: 'Sales Across Years', intervalType: 'Years' };
  public primaryyAxis: AxisModel = { title: 'Sales Amount in millions(USD)' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Applying Padding to the Range**

Padding can be applied to the minimum and maximum extremes of the range by using the
[`rangePadding`](../api/chart/axis/#rangepadding) property. Date time axis supports the
following types of padding,

* None
* Round
* Additional

**DateTime - None**

When the [`rangePadding`](../api/chart/axis/#rangepadding) is set to `None`, minimum and maximum of
the axis is based on the data.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', rangePadding: 'None' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**DateTime - Round**

When the [`rangePadding`](../api/chart/axis/#rangepadding) is set to `Round`, minimum and maximum
will be rounded to the nearest possible value divisible by interval.
For example, when the minimum is 15th Jan, interval is 1 and the interval type is ‘month’,
then the axis minimum will be Jan 1st.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', rangePadding: 'Round' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**DateTime - Additional**

When the [`rangePadding`](../api/chart/axis/#rangepadding) is set to `Additional`, interval of an axis will be
padded to the minimum and maximum of the axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', rangePadding: 'Additional' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Label Format

You can format and parse the date to all globalize format using [`labelFormat`](../api/chart/axis/#labelformat)
property in an axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { dateTimeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', labelFormat: 'yMd' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Average Sales Comparison'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dateTimeData} xName='x' yName='y' name='Sales' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
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