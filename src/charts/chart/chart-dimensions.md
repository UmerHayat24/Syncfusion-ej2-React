---
title: " Chart Appearance | React "

component: "Chart"

description: "We can set chart size manually by using width and height properties. We can set percentage or pixel size values to the chart."
---

# Chart Dimensions

## Size for Container

Chart can render to its container size. You can set the size via inline or CSS as demonstrated below.

```html
 <div id="charts" style="width:650px; height:350px"></div>
```

{% tab compileJsx=true%}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

  render(){
        return <ChartComponent id='charts'>
        </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

{% tab template="chart/dimensions/style", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, DataLabel,
  Inject, Legend,LineSeries, SeriesCollectionDirective, SeriesDirective,
  Tooltip} from '@syncfusion/ej2-react-charts';

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
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' type='Column' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Size for Chart

You can also set size for chart directly through [`width`](../api/chart/chartModel/#width) and
[`height`](../api/chart/chartModel/#height) properties.

<!-- markdownlint-disable MD036 -->
**In Pixel**
<!-- markdownlint-disable MD036 -->

You can set the size of chart in pixel as demonstrated below.

{% tab template= "chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, DataLabel,
  Inject, Legend,LineSeries, SeriesCollectionDirective, SeriesDirective,
  Tooltip} from '@syncfusion/ej2-react-charts';

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
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis} width='650' height='350'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' type='Column' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**In Percentage**

By setting value in percentage, chart gets its dimension with respect to its container. For example,
when the height is ‘50%’, chart renders to half of the container height.

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel,Category,ChartComponent, ColumnSeries, DataLabel,
  Inject, Legend,LineSeries, SeriesCollectionDirective, SeriesDirective,
  Tooltip} from '@syncfusion/ej2-react-charts';

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
    return <ChartComponent id='charts' primaryXAxis={this.primaryxAxis} width='80%' height='90%'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='month' yName='sales' type='Column' name='Sales' />
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

> Note:  When you do not specify the size, it takes `450px` as the height and window size as its width.