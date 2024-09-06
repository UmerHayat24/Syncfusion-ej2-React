---
title: " Chart Polar and Radar | React "

component: "Chart"

description: "Polar and Radar chart supports different draw types and customization to display the data."
---
<!-- markdownlint-disable MD036 -->

# Polar Chart and Radar Chart

## Polar Chart

To render a polar series, use series [`type`](../api/chart/series/#type) as `Polar` and
inject `PolarSeries` module into services

To get start quickly with React Polar and Radar Charts, you can check on this video:

`youtube:6kn9dCOla0c`

### Draw Types

Polar drawType property is used to change the series plotting type to line, column, area, range column,
spline, scatter, stacking area and stacking column. The default value of drawType is `Line`.

**Line**

To render a line draw type, use series [`drawType`](../api/chart/series/#drawtype) as `Line` and
inject `LineSeries` into services.

[`isClosed`](../api/chart/series/#isclosed) property specifies whether to join start and
end point of a line series used in polar chart to form a closed path. Default value of isClosed is true.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, LineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month' };
  public primaryyAxis: AxisModel = { minimum: 20, maximum: 40, interval: 5, title: 'Efficiency', labelFormat: '{value}%' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Efficiency of oil-fired power production'>
      <Inject services={[PolarSeries, LineSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' type='Polar' name='Department' drawType='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Spline**

To render a spline draw type, use series [`drawType`](../api/chart/series/#drawtype) as `Spline` and inject `SplineSeries` into services.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, Category, SplineSeries}
from'@syncfusion/ej2-react-charts';
import { splineData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: -5, maximum: 35, interval: 10, title: 'Temperature in Celsius', labelFormat: '{value}C' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Climate Graph-2012'>
      <Inject services={[PolarSeries, SplineSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={splineData} xName='x' yName='y' type='Polar' name='London' drawType='Spline'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Area**

To render a spline draw type in polar axis, use series [`drawType`](../api/chart/series/#drawtype)
as `Area` and inject `AreaSeries` into services.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, AreaSeries}
from'@syncfusion/ej2-react-charts';
import { areaData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', minimum: 1900, maximum: 2000, interval: 10 };
  public primaryyAxis: AxisModel = { minimum: 2, maximum: 5, interval: 0.5, title: 'Sales Amount in Millions' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[PolarSeries, AreaSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={areaData} xName='x' yName='y' type='Polar' name='London' drawType='Area' fill='#69D2E7'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Stacked Area**

To render a stacked area draw type, use series [`drawType`](../api/chart/series/#drawtype)
as `StackingArea` and inject `StackingAreaSeries` into services.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, StackingAreaSeries, Category}
from'@syncfusion/ej2-react-charts';
import { StackedAreaData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', valueType: 'Category', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 4, interval: 1, title: 'Spend Billions', majorTickLines: { width: 0 }, labelFormat: '{value}B' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Trend in Sales of Ethical Produce'>
      <Inject services={[PolarSeries, StackingAreaSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={StackedAreaData} xName='x' yName='y' type='Polar' name='Organic' drawType='StackingArea'></SeriesDirective>
        <SeriesDirective dataSource={StackedAreaData} xName='x' yName='y1' type='Polar' name='Fair -Trade' drawType='StackingArea'></SeriesDirective>
        <SeriesDirective dataSource={StackedAreaData} xName='x' yName='y2' type='Polar' name='Veg-Alternatives' drawType='StackingArea'></SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Column**

To render a spline draw type, use series [`drawType`](../api/chart/series/#drawtype) as `Column`
and inject `ColumnSeries` into services.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, Category, ColumnSeries}
from'@syncfusion/ej2-react-charts';
import { columnData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Country', valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Gold medals'>
      <Inject services={[PolarSeries, ColumnSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={columnData} xName='country' yName='gold' type='Polar' name='Gold' drawType='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacked Column**

To render a stacked column draw type, use series [`drawType`](../api/chart/series/#drawtype)
as `StackingColumn` and inject `StackingColumnSeries` into services.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, StackingColumnSeries, Category}
from'@syncfusion/ej2-react-charts';
import { stackedColumnData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 700, interval: 100, title: 'Spend Billions', labelFormat: '{value}B' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Mobile Game marker by Country'>
      <Inject services={[PolarSeries, StackingColumnSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stackedColumnData} xName='x' yName='y' type='Polar' name='England' drawType='StackingColumn'></SeriesDirective>
        <SeriesDirective dataSource={stackedColumnData} xName='x' yName='y1' type='Polar' name='Germany' drawType='StackingColumn'></SeriesDirective>
        <SeriesDirective dataSource={stackedColumnData} xName='x' yName='y2' type='Polar' name='France' drawType='StackingColumn'></SeriesDirective>
        <SeriesDirective dataSource={stackedColumnData} xName='x' yName='y3' type='Polar' name='Italy' drawType='StackingColumn'></SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Range Column**

To render a range column draw type, use series [`drawType`](../api/chart/series/#drawtype)
as `RangeColumn`.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, RangeColumnSeries, Category}
from'@syncfusion/ej2-react-charts';
import { rangeColumnData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'Temperature' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Maximum and Minimum Temperature'>
      <Inject services={[PolarSeries, RangeColumnSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective type='Polar' dataSource={rangeColumnData} xName='x' high='high' low='low' drawType='RangeColumn'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Scatter**

To render a scatter draw type, use series [`DrawType`](../api/chart/series/#drawtype) as `Scatter` and
inject `ScatterSeries` module into the service.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         PolarSeries, Category, ScatterSeries}
from'@syncfusion/ej2-react-charts';
import { scatterData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', valueType: 'Category' };
  public primaryyAxis: AxisModel = {
    minimum: -5, maximum: 35, interval: 10, title: 'Temperature in Celsius',
    labelFormat: '{value}C'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Climate Graph-2012'>
      <Inject services={[PolarSeries, ScatterSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={scatterData} xName='x' yName='y' type='Polar' name='London' drawType='Scatter'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Radar Chart

To render a Radar series, use series [`type`](../api/chart/series/#type) as `Radar` and
inject `RadarSeries` module into services

### Draw Type

Similar to Polar drawType, Radar draw type property is used to change the series plotting
type to line, column, area, range column, spline, scatter, stacking area and stacking column.
The default value of drawType is `Line`.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         RadarSeries, LineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month' };
  public primaryyAxis: AxisModel = { minimum: 20, maximum: 40, interval: 5, title: 'Efficiency', labelFormat: '{value}%' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Efficiency of oil-fired power production'>
      <Inject services={[RadarSeries, LineSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' type='Radar' name='Department' drawType='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

### Customization

**Start Angle**

You can customize the start angle of the polar series using
[`startAngle`](../api/chart/axis/#startangle) property. By default, `startAngle` is 0 degree.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         RadarSeries, LineSeries, ColumnSeries}
from'@syncfusion/ej2-react-charts';
import { columnData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', startAngle: 90 };
  public primaryyAxis: AxisModel = { minimum: 20, maximum: 40, interval: 5, title: 'Efficiency', labelFormat: '{value}%' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Efficiency of oil-fired power production'>
      <Inject services={[RadarSeries, LineSeries, ColumnSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={columnData} xName='x' yName='y' type='Radar' name='Department' drawType='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Coefficient in axis**

You can customize the radius of the polar series using
[`coefficient`](../api/chart/axis/#coefficient) property. By default, `coefficient` is 100.

{% tab template="chart/series/polar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         RadarSeries, LineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', coefficient: 90 };
  public primaryyAxis: AxisModel = { minimum: 20, maximum: 40, interval: 5, title: 'Efficiency', labelFormat: '{value}%' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Efficiency of oil-fired power production'>
      <Inject services={[RadarSeries, LineSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' type='Radar' name='Department' drawType='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}