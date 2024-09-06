---
title: " Financial charts | React "

component: "Chart"

description: "Financial charts are used to illustrate the movements in the price of a financial instrument over time. Chart have hilo, hiloopenclose,candle."
---

# Financial Charts

Financial charts are used to illustrate the movements in the price of a financial instrument over time.

To get start quickly with React Financial Charts, you can check on this video:

`youtube:nxcMqkfI-nA`

Chart supports the following financial series

<!-- markdownlint-disable MD036 -->

## Hilo

To render a Hilo series, use series [`type`](../api/chart/series/#type) as `Hilo` and inject `HiloSeries` module into the `services`.

{% tab template="chart/series/hilo", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
    HiloSeries, Category, Tooltip, ILoadedEventArgs, Zoom,
    Crosshair, ChartTheme }
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [
    { x: 'Jan', low: 87, high: 200 }, { x: 'Feb', low: 45, high: 135 },
    { x: 'Mar', low: 19, high: 85 }, { x: 'Apr', low: 31, high: 108 },
    { x: 'May', low: 27, high: 80 }, { x: 'June', low: 84, high: 130 },
    { x: 'July', low: 77, high: 150 }, { x: 'Aug', low: 54, high: 125 },
    { x: 'Sep', low: 60, high: 155 }, { x: 'Oct', low: 60, high: 180 },
    { x: 'Nov', low: 88, high: 180 }, { x: 'Dec', low: 84, high: 230 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Months' };
  public primaryyAxis: AxisModel = { labelFormat: '{value}mm', edgeLabelPlacement: 'Shift', title: 'Rainfall' };
  public style: any = { textAlign: "center" };
  public legendSettings: LegendSettingsModel = { visible: false };

  render() {
    return <ChartComponent id='charts' style={this.style}
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Maximum and Minimum Rainfall'>
      <Inject services={[HiloSeries, Tooltip, Category, Crosshair, Zoom]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='low' name='India' type='Hilo' low='low'
          high='high'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## High Low Open Close

To render a HiloOpenClose series, use series [`type`](../api/chart/series/#type) as `HiloOpenClose`
and inject `HiloOpenCloseSeries` module into the `services`.

{% tab template="chart/series/hiloOpenClose", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, HiloOpenCloseSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { Browser } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [
    { x: 'Jan', open: 120, high: 160, low: 100, close: 140 },
    { x: 'Feb', open: 150, high: 190, low: 130, close: 170 },
    { x: 'Mar', open: 130, high: 170, low: 110, close: 150 },
    { x: 'Apr', open: 160, high: 180, low: 120, close: 140 },
    { x: 'May', open: 150, high: 170, low: 110, close: 130 }
  ];
  public primaryxAxis: AxisModel = { title: 'Date', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20 };
  public style: any = { textAlign: "center" };
  public legendSettings: LegendSettingsModel = { visible: false };
  public border = { border: { width: 0 } };

  render() {
    return <ChartComponent id='charts' style={this.style}
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      chartArea={this.border}
      width={Browser.isDevice ? '100%' : '80%'}
      title='Financial Analysis'>
      <Inject services={[HiloOpenCloseSeries, Tooltip, Category, Crosshair, Zoom]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='low' name='SHIRPUR-G' type='HiloOpenClose' low='low'
          high='high' open='open' close='close'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customization of HiloOpenClose Series

In HiloOpenClose series, [`bullFillColor`](../api/chart/series#bullfillcolor) is used to fill the segment when
the open value is greater than the close value and [`bearFillColor`](../api/chart/series/#bearfillcolor) is
used to fill the segment when the open value is less than the close value.

{% tab template="chart/series/hiloOpenClose", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, HiloOpenCloseSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [
    { x: 'Jan', open: 120, high: 160, low: 100, close: 140 },
    { x: 'Feb', open: 150, high: 190, low: 130, close: 170 },
    { x: 'Mar', open: 130, high: 170, low: 110, close: 150 },
    { x: 'Apr', open: 160, high: 180, low: 120, close: 140 },
    { x: 'May', open: 150, high: 170, low: 110, close: 130 }
  ];
  public primaryxAxis: AxisModel = { title: 'Date', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20 };
  public style: any = { textAlign: "center" };
  public legendSettings: LegendSettingsModel = { visible: false };

  render() {
    return <ChartComponent id='charts' style={this.style}
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Financial Analysis'>
      <Inject services={[HiloOpenCloseSeries, Tooltip, Category, Crosshair, Zoom]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='low' name='SHIRPUR-G' type='HiloOpenClose' low='low'
          high='high' open='open' close='close' bearFillColor='#e56590' bullFillColor='#f8b883'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Candle

To render a Candle series, use series [`type`](../api/chart/series/#type) as `Candle` and inject `CandleSeries` module into the `services`.

{% tab template="chart/series/candle", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, CandleSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [
    { x: 'Jan', open: 120, high: 160, low: 100, close: 140 },
    { x: 'Feb', open: 150, high: 190, low: 130, close: 170 },
    { x: 'Mar', open: 130, high: 170, low: 110, close: 150 },
    { x: 'Apr', open: 160, high: 180, low: 120, close: 140 },
    { x: 'May', open: 150, high: 170, low: 110, close: 130 }
  ];
  public primaryxAxis: AxisModel = { title: 'Date', valueType: 'Category', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = { title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20 };
  public style: any = { textAlign: "center" };
  public legendSettings: LegendSettingsModel = { visible: false };

  render() {
    return <ChartComponent id='charts' style={this.style}
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Shirpur Gold Refinery Share Price'>
      <Inject services={[CandleSeries, Tooltip, Category, Crosshair, Zoom]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='low' name='SHIRPUR-G' type='Candle' low='low'
          high='high' open='open' close='close'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

### Hollow Candles

Candle charts allow to visually compare the current price with previous price by coloring them.

Candles are filled/left as hollow based on the following criteria.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>States</b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>Filled</td>
<td>candle sticks are filled when the close value is lesser than the open value</td>
</tr>
<tr>
<td>Unfilled</td>
<td>candle sticks are unfilled when the close value is greater than the open value</td>
</tr>
</table>

The color of the candle will be defined by comparing with previous values.
Bear color will be applied when the current closing value is greater than the previous closing value.
Bull color will be applied when the current closing value is less than the previous closing value.

By default, bullFillColor is set as red and bearFillColor is set as green.

### Solid Candles

[`enableSolidCandles`](../api/chart/series#enableSolidCandles-string) is used to enable/disable the solid candles.
By default is set to be false.
The fill color of the candle will be defined by its opening and closing values.

[`bearFillColor`](../api/chart/series#bearFillColor-string) will be applied when the opening value is less than the closing value.
[`bullFillColor`](../api/chart/series#bullFillColor-string) will be applied when the opening value is greater than closing value.

{% tab template="chart/series/candle", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, CandleSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [
    { x: 'Jan', open: 120, high: 160, low: 100, close: 140 },
    { x: 'Feb', open: 150, high: 190, low: 130, close: 170 },
    { x: 'Mar', open: 130, high: 170, low: 110, close: 150 },
    { x: 'Apr', open: 160, high: 180, low: 120, close: 140 },
    { x: 'May', open: 150, high: 170, low: 110, close: 130 }
  ];
  public primaryxAxis: AxisModel = { title: 'Date', valueType: 'Category', majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = { title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20 };
  public style: any = { textAlign: "center" };
  public legendSettings: LegendSettingsModel = { visible: false };

  render() {
    return <ChartComponent id='charts' style={this.style}
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Shirpur Gold Refinery Share Price'>
      <Inject services={[CandleSeries, Tooltip, Category, Crosshair, Zoom]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='low' name='SHIRPUR-G' type='Candle' low='low'
          high='high' open='open' close='close' bearFillColor='#e56590' bullFillColor='#f8b883'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}