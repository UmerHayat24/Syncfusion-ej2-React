---
title: " Chart Types | React "

component: "Chart"

description: "Essential JS 2 Chart  chart supports 32 types of series and also supports different tpes customizations for each type of chart."
---

# Chart Types

Essential JS 2 Chart supports 32 types of series.

<!-- markdownlint-disable MD036 -->

## Line Charts

<!-- markdownlint-disable MD036 -->
**Line**

To render a line series, use series [`type`](../api/chart/series/#type) as `Line` and inject `LineSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' width={2} name='India' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Step Line**

To render a step line series, use series [`type`](../api/chart/series/#type) as `StepLine` and
inject `StepLineSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StepLineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { steplineData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={steplineData} xName='x' yName='y' width={2} name='India' type='StepLine'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacked Line**

To render a stacked line series, use series [`type`](../api/chart/seriesModel/#type-string) as
`StackingLine` and inject `StackingLineSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingLineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[StackingLineSeries, Legend, Tooltip, DataLabel, Category]} />
                       primaryXAxis={{
                            interval: 1,  valueType: 'Category'
                        }}
                        primaryYAxis={{
                            title: 'Expense',
                            minimum: 0, maximum: 400, interval: 100,
                            labelFormat: '${value}',
                        }}
                        <SeriesCollectionDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y' name='John' width='2' type='StackingLine' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y1' name='Peter' width='2' type='StackingLine' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y2' name='Steve' width='2' type='StackingLine' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y3' name='Charle' width='2' type='StackingLine' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                        </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**100% Stacked Line**

To render a 100% stacked line series, use series [`type`](../api/chart/seriesModel/#type-string) as
`StackingLine100` and inject `StackingLineSeries`
module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingLineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[StackingLineSeries, Legend, Tooltip, DataLabel, Category]} />
                        primaryXAxis={{
                            interval: 1,  valueType: 'Category'
                        }}
                        primaryYAxis={{
                            title: 'Expense',
                            interval: 20,
                        }}
                        title='Family Expense for Month'
                        <SeriesCollectionDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y' name='John' width='2' type='StackingLine100' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y1' name='Peter' width='2' type='StackingLine100' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y2' name='Steve' width='2' type='StackingLine100' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                            <SeriesDirective dataSource={chartData} xName='x' yName='y3' name='Charle' width='2' type='StackingLine100' marker= {{visible: true}} dashArray='5,1'>
                            </SeriesDirective>
                        </SeriesCollectionDirective>
                    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Spline**

To render a spline series, use series [`type`](../api/chart/series/#type) as `Spline` and inject `SplineSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, SplineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { splineData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', valueType: 'Category' };
  public primaryyAxis: AxisModel = {
    minimum: -5, maximum: 35, interval: 5,
    title: 'Temperature in Celsius', labelFormat: '{value}C'
  };
  public marker = { visible: true, width: 10, height: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='CO2 - Intensity Analysis'>
      <Inject services={[SplineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={splineData} xName='x' yName='y' width={2} name='London' type='Spline'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Spline Area**

To render a spline series, use series [`type`](../api/chart/series/#type) as `Spline` and inject `SplineAreaSeries`
module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, SplineAreaSeries,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, SplineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { splineData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Month', valueType: 'Category' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[SplineAreaSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={splineData} xName='x' yName='y' width={2} name='London' type='SplineArea'
          marker={{ visible: true, width: 10, height: 10 }}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Multicolored Line**

To render a multicolored line series, use series [`type`](../api/chart/series/#type) as `Line` and
inject `LineSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, MultiColoredLineSeries, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [{ x: 2005, y: 28, color: 'red' }, { x: 2006, y: 25, color: 'green' },
                        { x: 2007, y: 26, color: '#ff0097' }, { x: 2008, y: 27, color: 'crimson' },
                        { x: 2009, y: 32, color: 'blue' }, { x: 2010, y: 35, color: 'darkorange' }];

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category, MultiColoredLineSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' width={2} name='India' type='MultiColoredLine'
          pointColorMapping='color'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Customization of Line Charts**

`stroke`, `stroke-width` and `dashArray` of all line type series can be customized by using [`fill`](../api/chart/series/#fill),
[`width`](../api/chart/series/#width) and [`dashArray`](../api/chart/series/#dasharray) properties.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' fill='green' width={3} dashArray='5,5'
          name='India' type='Line'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Area Charts

**Area**

To render a area series, use series [`type`](../api/chart/series/#type) as `Area` and inject `AreaSeries` module into the `services`.

{% tab template="chart/series/area", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, AreaSeries,  Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 1900, y: 4 }, { x: 1920, y: 3.0 }, { x: 1940, y: 3.8 },
    { x: 1960, y: 3.4 }, { x: 1980, y: 3.2 }, { x: 2000, y: 3.9 }
  ];
  public primaryxAxis: AxisModel = {
    title: 'Year', minimum: 1900, maximum: 2000, interval: 10,
    edgeLabelPlacement: 'Shift'};
  public primaryyAxis: AxisModel = { minimum: 2, maximum: 5, interval: 0.5, title: 'Sales Amount in Millions' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Product A' fill='#69D2E7'
          opacity={0.6} type='Area'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Spline Range Area**

The Spline Range Area Chart is used to display continuous data points as a set of splines that vary between high and low values over intervals of time and across different categories.

To render a spline range area series, use series [`type`](../api/chart/series/#type) as `SplineRangeArea` and inject `SplineRangeAreaSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, Category, SplineRangeAreaSeries} from'@syncfusion/ej2-react-charts';
import { splineRangeData } from 'datasource.ts';

class App extends React.Component<{}, {}> {
  
  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    edgeLabelPlacement: 'Shift',
    majorGridLines: { width: 0 }
  };
  public primaryyAxis: AxisModel = {
    labelFormat: '{value}˚C',
    lineStyle: { width: 0 },
    minimum: 0, maximum: 40,
    majorTickLines: { width: 0 }
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Monthly Temperature Range'>
      <Inject services={[SplineRangeAreaSeries, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={splineRangeData} xName='x' high='high' low='low' name='England' opacity={0.4} type='SplineRangeArea'>
        </SeriesDirective>
        <SeriesDirective dataSource={splineRangeData} xName='x' high='high1' low='low1' name='India' opacity={0.4} type='SplineRangeArea'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacked Area**

To render a stacked area series, use series [`type`](../api/chart/series/#type) as `StackingArea`
and inject `StackingAreaSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, StackingAreaSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { stackedData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Years', valueType: 'DateTime', intervalType: 'Years',
    majorTickLines: { width: 0 }, labelFormat: 'y', edgeLabelPlacement: 'Shift'};
  public primaryyAxis: AxisModel = {
    title: 'Spend in Billions', minimum: 0, maximum: 7, interval: 1,
    majorTickLines: { width: 0 }, labelFormat: '{value}B'};

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Trend in Sales of Ethical Produce'>
      <Inject services={[StackingAreaSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stackedData} xName='x' yName='y' name='Organic' type='StackingArea'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackedData} xName='x' yName='y1' name='Fair-trade' type='StackingArea'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackedData} xName='x' yName='y2' name='Veg Alternatives' type='StackingArea'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackedData} xName='x' yName='y3' name='Others' type='StackingArea'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**100% Stacked Area**

To render a 100% stacked area series, use series [`type`](../api/chart/series/#type) as
`StackingArea100` and inject `StackingAreaSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, Zoom, Crosshair, StackingAreaSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { percentData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Years', valueType: 'DateTime', intervalType: 'Years',
    edgeLabelPlacement: 'Shift', labelFormat: 'y'};
  public primaryyAxis: AxisModel = { title: 'Temperature (%)', labelFormat: '{value}%', rangePadding: 'None' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Annual Temperature Comparison'>
      <Inject services={[StackingAreaSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={percentData} xName='x' yName='y' name='USA' type='StackingArea100'>
        </SeriesDirective>
        <SeriesDirective dataSource={percentData} xName='x' yName='y1' name='UK' type='StackingArea100'>
        </SeriesDirective>
        <SeriesDirective dataSource={percentData} xName='x' yName='y2' name='Canada Alternatives' type='StackingArea100'>
        </SeriesDirective>
        <SeriesDirective dataSource={percentData} xName='x' yName='y3' name='China' type='StackingArea100'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Step Area**

To render a step area series, use series [`type`](../api/chart/series/#type) as
`StepArea` and inject `StepAreaSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, StepAreaSeries}
from'@syncfusion/ej2-react-charts';
import { stepAreaData } from 'datasource.ts';

class App extends React.Component<{}, {}> {
  public primaryxAxis: AxisModel = { valueType: 'Double', title: 'Overs' };
  public primaryyAxis: AxisModel = { title: 'Runs' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Annual Temperature Comparison'>
      <Inject services={[StepAreaSeries, Legend]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stepAreaData} xName='x' yName='y' name='England' type='StepArea'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacked Step Area**

To render a stacked step area series, use series `type` as `StackingStepArea` and inject `StackingStepAreaSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, StackingStepAreaSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {
  
  public data1: object [] = [
                { x: 2000, y: 416 }, { x: 2001, y: 490 }, { x: 2002, y: 470 }, { x: 2003, y: 500 },
                { x: 2004, y: 449 }, { x: 2005, y: 470 }, { x: 2006, y: 437 }, { x: 2007, y: 458 },
                { x: 2008, y: 500 }, { x: 2009, y: 473 }, { x: 2010, y: 520 }, { x: 2011, y: 509 }
  ];
  public data2: object [] = [
                { x: 2000, y: 180 }, { x: 2001, y: 240 }, { x: 2002, y: 370 }, { x: 2003, y: 200 },
                { x: 2004, y: 229 }, { x: 2005, y: 210 }, { x: 2006, y: 337 }, { x: 2007, y: 258 },
                { x: 2008, y: 300 }, { x: 2009, y: 173 }, { x: 2010, y: 220 }, { x: 2011, y: 309 }
  ];
  render() {
    return <ChartComponent id='charts'>
      <Inject services={[StackingStepAreaSeries, Legend]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data1} xName='x' yName='y' type='StackingStepArea'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data2} xName='x' yName='y' type='StackingStepArea'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Multicolored area**

To render a multicolored area series, use the series type as `MultiColoredArea`, and inject
the `MultiColoredAreaSeries` module into the `services`. The required `segments` of the series can be customized
using the `value`, `color`, and `dashArray`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, MultiColoredAreaSeries, SegmentsDirective,
         Legend, StepAreaSeries, SegmentDirective }
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [{ x: 2005, y: 28 }, { x: 2006, y: 25 }, { x: 2007, y: 26 }, { x: 2008, y: 27 },
                        { x: 2009, y: 32 }, { x: 2010, y: 35 }, { x: 2011, y: 25 }]

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[StepAreaSeries, Legend, MultiColoredAreaSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='England' type='MultiColoredArea' segmentAxis='X' >
          <SegmentsDirective>
            <SegmentDirective value={2007} color='blue'></SegmentDirective>
            <SegmentDirective value={2009} color='green'></SegmentDirective>
            <SegmentDirective color='orange'></SegmentDirective>
          </SegmentsDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Customization of Area Charts**

`fill`, `border` and `dashArray` of all area type series can be customized
using [`fill`](../api/chart/series/#fill),
[`border`](../api/chart/series/#border)
and [`dashArray`](../api/chart/series/#dasharray) properties.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, AreaSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { areaData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Year', minimum: 1900, maximum: 2000, interval: 10,
    edgeLabelPlacement: 'Shift'
  };
  public primaryyAxis: AxisModel = { minimum: 2, maximum: 5, interval: 0.5, title: 'Sales Amount in Millions' };
  public border = { color: 'red', width: 2 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={areaData} xName='x' yName='y' name='Product A'
          fill='green' width={2} dashArray='5,5' border={this.border}
          opacity={0.6} type='Area'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Column Charts

**Column**

To render a column series, use series [`type`](../api/chart/series/#type) as `Column` and inject `ColumnSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { columnData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={columnData} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacked Column**

To render a stacked column series, use series [`type`](../api/chart/series/#type) as
`StackingColumn` and inject`StackingColumnSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { stackColumndata } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', interval: 1, valueType: 'Category' };
  public primaryyAxis: AxisModel = {
    title: 'Sales in Billions', minimum: 0, maximum: 700, interval: 100,
    labelFormat: '{value}B'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Mobile Game Market by Country'>
      <Inject services={[StackingColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y' name='UK' type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y1' name='Germany' type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y2' name='France' type='StackingColumn'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y3' name='Italy' type='StackingColumn'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**100% Stacked Column**

To render a 100% stacked column series, use series [`type`](../api/chart/series/#type) as
`StackingColumn100` and inject `StackingColumnSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { columnperData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', interval: 1, valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'GDP (%) Per Annum', rangePadding: 'None', labelFormat: '{value}%' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Gross Domestic Product Growth'>
      <Inject services={[StackingColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={columnperData} xName='x' yName='y' name='UK' type='StackingColumn100'>
        </SeriesDirective>
        <SeriesDirective dataSource={columnperData} xName='x' yName='y1' name='Germany' type='StackingColumn100'>
        </SeriesDirective>
        <SeriesDirective dataSource={columnperData} xName='x' yName='y2' name='France' type='StackingColumn100'>
        </SeriesDirective>
        <SeriesDirective dataSource={columnperData} xName='x' yName='y3' name='Italy' type='StackingColumn100'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Range Column**

To render a range column series, use series [`type`](../api/chart/series/#type) as `RangeColumn`
and inject `RangeColumnSeries` module into the `services`.

{% tab template="chart/series/rangecolumn", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, RangeColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public data: any[] = [
             { x: 'Jan', low: 0.7, high: 6.1 }, { x: 'Feb', low: 1.3, high: 6.3 }, { x: 'Mar', low: 1.9, high: 8.5 },
             { x: 'Apr', low: 3.1, high: 10.8 }, { x: 'May', low: 5.7, high: 14.40 }, { x: 'Jun', low: 8.4, high: 16.90 },
             { x: 'Jul', low: 10.6,high: 19.20 }, { x: 'Aug', low: 10.5,high: 18.9 }, { x: 'Sep', low: 8.5, high: 16.1 },
             { x: 'Oct', low: 6.0, high: 12.5 }, { x: 'Nov', low: 1.5, high: 6.9  }, { x: 'Dec', low: 5.1, high: 12.1 }
        ];
    public data1: any[]= [
             { x: 'Jan', low: 1.7, high: 7.1 }, { x: 'Feb', low: 1.9, high: 7.7 }, { x: 'Mar', low: 1.2, high: 7.5 },
             { x: 'Apr', low: 2.5, high: 9.8 }, { x: 'May', low: 4.7, high: 11.4 }, { x: 'Jun', low: 6.4, high: 14.4 },
             { x: 'Jul', low: 9.6, high: 17.2 }, { x: 'Aug', low: 10.7, high: 17.9 }, { x: 'Sep', low: 7.5, high: 15.1 },
             { x: 'Oct', low: 3.0, high: 10.5 }, { x: 'Nov', low: 1.2, high: 7.9 }, { x: 'Dec', low: 4.1, high: 9.1 }
        ];
    public primaryxAxis: AxisModel= {valueType: 'Category', title: 'month'}  ;
    public primaryyAxis: AxisModel= { title: 'Temperature(Celsius)'}  ;

    render(){
        return <ChartComponent id='charts'
                primaryXAxis={ this.primaryxAxis }
                primaryYAxis={ this.primaryyAxis }
                title='Maximum and minimum Temperature'>
                  <Inject services={[RangeColumnSeries, Legend, Tooltip, DataLabel,  Category]}/>
                  <SeriesCollectionDirective>
                      <SeriesDirective dataSource ={this.data}  xName='x' low='low' high='high' type='RangeColumn'>
                      </SeriesDirective>
                      <SeriesDirective dataSource ={this.data1}  xName='x' low='low' high='high' type='RangeColumn'>
                      </SeriesDirective>
                   </SeriesCollectionDirective>
              </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Customization of Column**

<!-- markdownlint-disable MD013 -->
`fill` and `border` of all column type series can be
customized using [`fill`](../api/chart/series/#fill) and [`border`](../api/chart/series/#border) properties.
Width of the column and space between each column can be customized using [`columnWidth`](../api/chart/series/#columnwidth) and [`columnSpacing`](../api/chart/series/#columnspacing) properties respectively. The [`columnWidthInPixel`](../api/chart/series/#columnwidthinpixel) property allows to specify the column width in pixel unit.
For customizing a specify point, please refer the
[`pointRender`](../api/chart/chartModel/#pointrender).

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { columnData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public border = { color: 'green', width: 2 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={columnData} xName='country' yName='gold' name='Gold' type='Column'
          fill='red' border={this.border} columnWidth={0.5} columnSpacing={0.7}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacking Group**

You can use the [`stackingGroup`](../api/chart/series/#stackinggroup) property to group the stacked columns and 100% stacked columns.
Columns with same group name are stacked on top of each other.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { stackColumndata } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', interval: 1, valueType: 'Category' };
  public primaryyAxis: AxisModel = {
    title: 'Sales in Billions', minimum: 0, maximum: 700, interval: 100,
    labelFormat: '{value}B'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Mobile Game Market by Country'>
      <Inject services={[StackingColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y' name='UK' type='StackingColumn'
          stackingGroup='a'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y1' name='Germany' type='StackingColumn'
          stackingGroup='a'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y2' name='France' type='StackingColumn'
          stackingGroup='b'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackColumndata} xName='x' yName='y3' name='Italy' type='StackingColumn'
          stackingGroup='b'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Grouped Column**

You can use the [`groupName`](../api/chart/series/#groupname) property to group the data points in the column type charts. Data points with same group name are grouped together.

{% tab template="chart/series/group-column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  ChartComponent,
  SeriesCollectionDirective,
  SeriesDirective,
  Inject,
  Legend,
  Category,
  Tooltip,
  ColumnSeries,
  DataLabel }
from'@syncfusion/ej2-react-charts';

export let data1 = [
  { x: '2012', y: 104 },
  { x: '2016', y: 121 },
  { x: '2020', y: 113 },
];
export let data2 = [
  { x: '2012', y: 46 },
  { x: '2016', y: 46 },
  { x: '2020', y: 39 },
];
export let data3 = [
  { x: '2012', y: 65 },
  { x: '2016', y: 67 },
  { x: '2020', y: 65 },
];
export let data4 = [
  { x: '2012', y: 29 },
  { x: '2016', y: 27 },
  { x: '2020', y: 22 },
];
export let data5 = [
  { x: '2012', y: 91 },
  { x: '2016', y: 70 },
  { x: '2020', y: 88 },
];
export let data6 = [
  { x: '2012', y: 38 },
  { x: '2016', y: 26 },
  { x: '2020', y: 38 },
];
class App extends React.Component<{}, {}> {
  render() {
    return (
      <ChartComponent
        id="charts"
        style={{ textAlign: 'center' }}
        primaryXAxis={{
          valueType: 'Category',
          interval: 1,
          majorGridLines: { width: 0 },
        }}
        primaryYAxis={{
          majorGridLines: { width: 0 },
          majorTickLines: { width: 0 },
          lineStyle: { width: 0 },
          labelStyle: { color: 'transparent' },
        }}
        chartArea={{ border: { width: 0 } }}
        tooltip={{ enable: true }}
        title="Olympics Medal Tally"
      >
        <Inject
          services={[ColumnSeries, Legend, Tooltip, Category, DataLabel]}
        />
        <SeriesCollectionDirective>
          <SeriesDirective
            dataSource={data1}
            xName="x"
            yName="y"
            name="USA Total"
            type="Column"
            groupName="USA"
            columnWidth={0.7}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data2}
            xName="x"
            yName="y"
            name="USA Gold"
            type="Column"
            groupName="USA"
            columnWidth={0.5}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data3}
            xName="x"
            yName="y"
            name="UK Total"
            type="Column"
            groupName="UK"
            columnWidth={0.7}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data4}
            xName="x"
            yName="y"
            name="UK Gold"
            type="Column"
            groupName="UK"
            columnWidth={0.5}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data5}
            xName="x"
            yName="y"
            name="China Total"
            type="Column"
            groupName="China"
            columnWidth={0.7}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data6}
            xName="x"
            yName="y"
            name="China Gold"
            type="Column"
            groupName="China"
            columnWidth={0.5}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
        </SeriesCollectionDirective>
      </ChartComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Bar Chart

**Bar**

To render a bar series, use series [`type`](../api/chart/series/#type) as `Bar` and inject `BarSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, BarSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = {
    minimum: 3, maximum: 12, interval: 1, title: 'Percentage',
    labelFormat: '{value}%'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[BarSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='India' type='Bar'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacked bar**

To render a stacked bar series, use series [`type`](../api/chart/series/#type) as `StackingBar` and inject `StackingBarSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingBarSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { stackBarData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Months' };
  public primaryyAxis: AxisModel = {
    title: 'Percentage (%)', minimum: -20, maximum: 100,
    edgeLabelPlacement: 'Shift', labelFormat: '{value}%'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Sales Comparison'>
      <Inject services={[StackingBarSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stackBarData} xName='x' yName='y' name='Apple' type='StackingBar'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackBarData} xName='x' yName='y1' name='orange' type='StackingBar'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackBarData} xName='x' yName='y2' name='Wastage' type='StackingBar'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**100% Stacked Bar**

To render a 100% stacked bar series, use series [`type`](../api/chart/series/#type) as `StackingBar100` and inject `StackingBarSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingBarSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { stackBarData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Months' };
  public primaryyAxis: AxisModel = {
    title: 'Percentage (%)', minimum: -20, maximum: 100,
    edgeLabelPlacement: 'Shift', labelFormat: '{value}%'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Sales Comparison'>
      <Inject services={[StackingBarSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stackBarData} xName='x' yName='y' name='Apple' type='StackingBar100'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackBarData} xName='x' yName='y1' name='orange' type='StackingBar100'>
        </SeriesDirective>
        <SeriesDirective dataSource={stackBarData} xName='x' yName='y2' name='Wastage' type='StackingBar100'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Customization of Bar Series**

`fill` and `border` of all bar type series can be
customized using [`fill`](../api/chart/series/#fill) and [`border`](../api/chart/series/#border).
Width of the bar and space between each bar can be customized using [`columnWidth`](../api/chart/series/#columnwidth) and [`columnSpacing`](../api/chart/series/#columnspacing) properties respectively. The [`columnWidthInPixel`](../api/chart/series/#columnwidthinpixel) property allows to specify the bar width in pixel unit.
For customizing a specify point, please refer the
[`pointRender`](../api/chart/chartModel/#pointrender).

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, BarSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { customData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = {
    minimum: 3, maximum: 12, interval: 1, title: 'Percentage',
    labelFormat: '{value}%'
  };
  public border = { color: 'green', width: 2 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[BarSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={customData} xName='x' yName='y' name='India' type='Bar'
          columnWidth={0.5}
            columnSpacing={0.7} fill='red' border={this.border}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Stacking Group**

You can use the [`stackingGroup`](../api/chart/series/#stackinggroup) property to group the stacked bar and 100% stacked bar.
Columns with same group name are stacked on top of each other.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, StackingBarSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { groupData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Year', minimum: 2006, maximum: 2015, interval: 1 };
  public primaryyAxis: AxisModel = { title: 'Sales Percentage(%)' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Sales by year'>
      <Inject services={[StackingBarSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={groupData} xName='x' yName='y' name='John' type='StackingBar'
          stackingGroup='JohnandAndrew'>
        </SeriesDirective>
        <SeriesDirective dataSource={groupData} xName='x' yName='y1' name='Andrew' type='StackingBar'
          stackingGroup='JohnandAndrew'>
        </SeriesDirective>
        <SeriesDirective dataSource={groupData} xName='x' yName='y2' name='Thomas' type='StackingBar'
          stackingGroup='ThomasandMichael'>
        </SeriesDirective>
        <SeriesDirective dataSource={groupData} xName='x' yName='y3' name='Michael' type='StackingBar'
          stackingGroup='ThomasandMichael'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Grouped Bar**

You can use the [`groupName`](../api/chart/series/#groupname) property to group the data points in the Bar type charts. Data points with same group name are grouped together.

{% tab template="chart/series/group-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  ChartComponent,
  SeriesCollectionDirective,
  SeriesDirective,
  Inject,
  Legend,
  Category,
  Tooltip,
  BarSeries,
  DataLabel }
from'@syncfusion/ej2-react-charts';

export let data1 = [
  { x: '2012', y: 104 },
  { x: '2016', y: 121 },
  { x: '2020', y: 113 },
];
export let data2 = [
  { x: '2012', y: 46 },
  { x: '2016', y: 46 },
  { x: '2020', y: 39 },
];
export let data3 = [
  { x: '2012', y: 65 },
  { x: '2016', y: 67 },
  { x: '2020', y: 65 },
];
export let data4 = [
  { x: '2012', y: 29 },
  { x: '2016', y: 27 },
  { x: '2020', y: 22 },
];
export let data5 = [
  { x: '2012', y: 91 },
  { x: '2016', y: 70 },
  { x: '2020', y: 88 },
];
export let data6 = [
  { x: '2012', y: 38 },
  { x: '2016', y: 26 },
  { x: '2020', y: 38 },
];
class App extends React.Component<{}, {}> {
  render() {
    return (
      <ChartComponent
        id="charts"
        style={{ textAlign: 'center' }}
        primaryXAxis={{
          valueType: 'Category',
          interval: 1,
          majorGridLines: { width: 0 },
        }}
        primaryYAxis={{
          majorGridLines: { width: 0 },
          majorTickLines: { width: 0 },
          lineStyle: { width: 0 },
          labelStyle: { color: 'transparent' },
        }}
        chartArea={{ border: { width: 0 } }}
        tooltip={{ enable: true }}
        title="Olympics Medal Tally"
      >
        <Inject
          services={[BarSeries, Legend, Tooltip, Category, DataLabel]}
        />
        <SeriesCollectionDirective>
          <SeriesDirective
            dataSource={data1}
            xName="x"
            yName="y"
            name="USA Total"
            type="Bar"
            groupName="USA"
            columnWidth={0.7}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data2}
            xName="x"
            yName="y"
            name="USA Gold"
            type="Bar"
            groupName="USA"
            columnWidth={0.5}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data3}
            xName="x"
            yName="y"
            name="UK Total"
            type="Bar"
            groupName="UK"
            columnWidth={0.7}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data4}
            xName="x"
            yName="y"
            name="UK Gold"
            type="Bar"
            groupName="UK"
            columnWidth={0.5}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data5}
            xName="x"
            yName="y"
            name="China Total"
            type="Bar"
            groupName="China"
            columnWidth={0.7}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
          <SeriesDirective
            dataSource={data6}
            xName="x"
            yName="y"
            name="China Gold"
            type="Bar"
            groupName="China"
            columnWidth={0.5}
            columnSpacing={0.1}
            marker={{
              dataLabel: {
                visible: true,
                position: 'Top',
                font: { fontWeight: '600', color: '#ffffff' },
              },
            }}
          ></SeriesDirective>
        </SeriesCollectionDirective>
      </ChartComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Scatter Charts

To render a scatter series, use series [`type`](../api/chart/series/#type) as `Scatter` and inject `ScatterSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ScatterSeries, Marker}
from'@syncfusion/ej2-react-charts';
import { scatterData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Height (cm)', minimum: 130, maximum: 180,
    edgeLabelPlacement: 'Shift', labelFormat: '{value}cm'
  };
  public primaryyAxis: AxisModel = {
    title: 'Weight (kg)', minimum: 30, maximum: 100,
    labelFormat: '{value}kg', rangePadding: 'None'
  };
  public marker = { width: 15, height: 15 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Height Vs Weight'>
      <Inject services={[ScatterSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={scatterData} xName='height' yName='male' name='Male' type='Scatter'
          marker={this.marker}>
        </SeriesDirective>
        <SeriesDirective dataSource={scatterData} xName='height' yName='female' name='Female' type='Scatter'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Bubble Chart

To render a bubble series, use series [`type`](../api/chart/series/#type) as `Bubble` and inject `BubbleSeries` module into the `services`.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         BubbleSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

  public data: any[] = [
        { x: 92.2, y: 7.8, size: 1.347, text: 'China' },
        { x: 74, y: 6.5, size: 1.241, text: 'India' },
        { x: 90.4, y: 6.0, size: 0.238, text: 'Indonesia' },
        { x: 99.4, y: 2.2, size: 0.312, text: 'US' },
        { x: 88.6, y: 1.3, size: 0.197, text: 'Brazil' },
        { x: 99, y: 0.7, size: 0.0818, text: 'Germany' },
        { x: 72, y: 2.0, size: 0.0826, text: 'Egypt' },
        { x: 99.6, y: 3.4, size: 0.143, text: 'Russia' },
        { x: 99, y: 0.2, size: 0.128, text: 'Japan' },
        { x: 86.1, y: 4.0, size: 0.115, text: 'Mexico' },
        { x: 92.6, y: 6.6, size: 0.096, text: 'Philippines' },
        { x: 61.3, y: 14.5, size: 0.162, text: 'Nigeria' }
];
public primaryxAxis: AxisModel= { title: 'Literacy Rate', minimum: 60, maximum: 100, interval: 5 }  ;
public primaryyAxis: AxisModel= { title: 'GDP growth rate', minimum: -2, maximum: 16, interval: 2 }  ;

render(){
  return <ChartComponent id='charts'
           primaryXAxis={ this.primaryxAxis }
           primaryYAxis={ this.primaryyAxis }
           title='GDP vs Literacy Rate'>
            <Inject services={[BubbleSeries]}/>
            <SeriesCollectionDirective>
                <SeriesDirective dataSource ={this.data}  xName='x' yName='y' size='size' type='Bubble' name='pound'>
                </SeriesDirective>
            </SeriesCollectionDirective>
          </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Bubble Size Mapping**

`size` property can be used to map the size value specified in data source.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         BubbleSeries}
from'@syncfusion/ej2-react-charts';
import { bubbleData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  render() {
    return <ChartComponent id='charts'>
      <Inject services={[BubbleSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={bubbleData} xName='x' yName='y' size='size' type='Bubble'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## See Also

* [Data label](./data-labels/)
* [Tooltip](./tool-tip/)