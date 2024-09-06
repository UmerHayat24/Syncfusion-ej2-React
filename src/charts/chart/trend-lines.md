---
title: " Chart Trendlines | React "

component: "Chart"

description: "Trendlines are used to show the direction and speed of price. Chart supports 6 types of trendlines and also provides trendlines customization."
---
<!-- markdownlint-disable MD036 -->

# Trendlines

Trendlines are used to show the direction and speed of price.

Trendlines can be generated for Cartesian type series (Line, Column, Scatter, Area,
Candle, Hilo etc.) except bar type series. You can add more than one trendline to a series.

Chart supports 6 types of trendlines.

## Linear

A linear trendline is a best fit straight line that is used with simpler data sets. To render a linear trendline,
use trendline [`type`](../api/chart/trendlineModel/#type) as `Linear` and inject
`Trendlines` module using `Chart.Inject(Trendlines)`.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Linear' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Exponential

An exponential trendline is a curved line that is most useful when data values rise or fall at increasingly higher rates.
You cannot create an exponential trendline, if your data contains zero or negative values.

To render a exponential trendline,
use trendline [`type`](../api/chart/trendlineModel/#type) as `Exponential` and inject
`Trendlines` module using `Chart.Inject(Trendlines)`.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Exponential' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Logarithmic

A logarithmic trendline is a best-fit curved line that is most useful
when the rate of change in the data increases or decreases quickly and then levels out.
A logarithmic trendline can use negative and/or positive values.

To render a logarithmic trendline, use trendline [`type`](../api/chart/trendlineModel/#type) as `Logarithmic` and inject
`Trendlines` module using `Chart.Inject(Trendlines)`.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Logarithmic' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Polynomial

A polynomial trendline is a curved line that is used when data fluctuates.

To render a polynomial trendline,
use trendline [`type`](../api/chart/trendlineModel/#type) as `Polynomial` and inject
`Trendlines` module using `Chart.Inject(Trendlines)`.

`polynomialOrder` used to define the polynomial value.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Polynomial' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Power

A power trendline is a curved line that is best used with data sets that compare measurements that increase at a specific rate.

To render a power trendline, use trendline [`type`](../api/chart/trendlineModel/#type) as `Power` and inject
`Trendlines` module using `Chart.Inject(Trendlines)`.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public powerData: object[] = [
    { x: 1, y: 10 }, { x: 2, y: 50 }, { x: 3, y: 80 }, { x: 4, y: 110 },
    { x: 5, y: 180 }, { x: 6, y: 220 }, { x: 7, y: 300 }, { x: 8, y: 370 }, { x: 9, y: 490 }, { x: 10, y: 500 }
  ];
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 50,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.powerData} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Power' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Moving Average

A moving average trendline smoothen out fluctuations in data to show a pattern or trend more clearly.

To render a moving average trendline, use trendline [`type`](../api/chart/trendlineModel/#type) as `MovingAverage` and inject
`Trendlines` module using `Chart.Inject(Trendlines)`.

`period` property defines the period to find the moving average.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='MovingAverage' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customization of Trendline**

The [`fill`](../api/chart/trendlineModel/#fill) and
[`width`](../api/chart/trendlineModel/#width) properties are used to customize the appearance of the trendline.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Linear' fill='red' width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Forecasting

Trendline forecasting is the prediction of future/past situations.

Forward Forecasting and Backward Forecasting are the two types of forecasting.

**Forward Forecasting**

The value set for forwardForecast is used to determine the distance moving towards the future trend.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Linear' backwardForecast={5} width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Backward Forecasting**

The value set for the backwardForecast is used to determine the past trends.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';


class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective type='Linear' backwardForecast={5} width={3} marker={this.marker}>
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Show or hide a trendline

You can show or hide the trendline by setting trendline `visible` property.

{% tab template= "chart/series/trendlines",  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, TrendlineDirective, TrendlinesDirective, Inject,
    Tooltip, LineSeries, ScatterSeries, SplineSeries, Trendlines, Category, ChartTheme
    ,AxisModel,TooltipSettingsModel,ChartAreaModel
} from '@syncfusion/ej2-react-charts';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { SampleBase } from '../common/sample-base';
import { PropertyPane } from '../common/property-pane';
import { EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public series1: Object[] = [];
  public yValue: number[] = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
  public chartLoad(): void {
    let i: number;
    let j: number = 0;
    for (i = 1973; i <= 2013; i++) {
      this.series1.push({ x: i, y: this.yValue[j] });
      j++;
    }
  }
  public primaryxAxis: AxisModel = { title: 'Months', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {
    title: 'Rupees against Dollars', interval: 10,
    lineStyle: { width: 0 }, majorTickLines: { width: 0 }
  };
  public tooltip: TooltipSettingsModel = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public marker = { visible: false };

  render() {
    this.chartLoad();
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      chartArea={this.chartarea}
      title='Historical Indian Rupee Rate (INR USD)'>
      <Inject services={[Category, Tooltip, ScatterSeries, SplineSeries, LineSeries, Trendlines]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' name='Apple Inc' type='Scatter' fill='#0066FF'>
          <TrendlinesDirective>
            <TrendlineDirective  type='Linear' visible={false} >
            </TrendlineDirective>
          </TrendlinesDirective>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}