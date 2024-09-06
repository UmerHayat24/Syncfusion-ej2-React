---
title: " Chart Technical Indicators | React "

component: "Chart"

description: "Indicators represent a statistical approach to technical analysis as opposed to a subjective approach. we have different types of indicators."
---
<!-- markdownlint-disable MD036 -->

# Technical Indicators

A technical indicator is a mathematical calculation based on historic price, volume or open interest information
that aims to forecast financial market direction.

Chart supports 10 types of technical indicators.

## Accumulation Distribution

Accumulation Distribution combines price and volume to show how money may be flowing into or out of stock.
To render a Accumulation Distribution Indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as `AccumulationDistribution` and inject
`AccumulationDistributionIndicator` into services.
To calculate the signal line [`volume`](../api/chart/technicalIndicatorModel/#volume) field is additionally added with `dataSource`.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true, sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {AxisModel,ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLineDirective,ChartAreaModel,CrosshairSettingsModel,
    Crosshair, LineSeries, AccumulationDistributionIndicator, IAxisLabelRenderEventArgs,TooltipSettingsModel,
    StripLine, ChartTheme, IndicatorsDirective, IndicatorDirective, StripLinesDirective}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public axisLableRender = (args: IAxisLabelRenderEventArgs): void => {
    if (args.axis.name === 'secondary') {
      let value: number = Number(args.text) / 1000000000;
      args.text = String(value) + 'bn';
    }
  }
  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      axisLabelRender={this.axisLableRender.bind(this)}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, AccumulationDistributionIndicator]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true}
          majorGridLines={this.lines} majorTickLines={this.lines} minimum={-7000000000} maximum={5000000000}
          interval={6000000000} title='Accumulation Distribution' lineStyle={this.lines}>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='AccumulationDistribution' field='Close' seriesName='Apple Inc' yAxisName='secondary' fill='#6063ff' period={3} animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Average True Range (ATR)

ATR measures the stock volatility by comparing the current value with the previous value.
To render a Average True Range (ATR) Indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as `Atr` and inject `AtrIndicator` into services

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLinesDirective, StripLineDirective,
    Crosshair, LineSeries, AtrIndicator, StripLine, ChartTheme, IndicatorsDirective, IndicatorDirective
    ,AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, AtrIndicator]} />
      <AxesDirective>
        <AxisDirective name='secondary'
          opposedPosition={true} rowIndex={0}
          majorGridLines={this.lines} lineStyle={this.lines} majorTickLines={this.lines}
          maximum={14} minimum={0} interval={7} title={'ATR'}>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective yAxisName='secondary' type='Atr' fill='#6063ff' seriesName='Apple Inc' period={3}
          animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Bollinger Band

A chart overlay that shows the upper and lower limits of normal price movements based on the standard deviation of prices.
To render a Bollinger Band, use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as `BollingerBand`
and inject `BollingerBands` module and `RangeAreaSeries` into services.
Bollinger band will be represented by three lines (upperLine, lowerLine, signalLine).
The default values of the Bollinger Band [`period`](../api/chart/technicalIndicatorModel/#period) is 14 and
[`standardDeviations`](../api/chart/technicalIndicatorModel/#standarddeviation) is 2.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject, StripLineDirective, StripLine, StripLinesDirective,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic,
    Crosshair, LineSeries, BollingerBands, ChartTheme, IndicatorsDirective, IndicatorDirective, RangeAreaSeries,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public upperline = { color: '#ffb735', width: 1 };
  public lowerline = { color: '#f2ec2f', width: 1 };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, BollingerBands, RangeAreaSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='BollingerBands' field='Close' seriesName='Apple Inc' fill='#606eff'
          period={14} animation={this.animation} upperLine={this.upperline} lowerLine={this.lowerline}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customization of BollingerBand**

`stroke`, `stroke-width`, and `color` of upperLine can be customized by using,[`upperLine`](../api/chart/technicalIndicatorModel/#upperline),
and the lowerLine can be customized by using [`lowerLine`](../api/chart/technicalIndicatorModel/#lowerline) properties of indicator.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject, StripLineDirective, StripLine, StripLinesDirective,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic,
    Crosshair, LineSeries, BollingerBands, ChartTheme, IndicatorsDirective, IndicatorDirective, RangeAreaSeries,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public upperline = { color: 'orange' };
  public lowerline = { color: 'yellow' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.crosshair}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, BollingerBands]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='BollingerBands' field='Close' seriesName='Apple Inc' fill='#606eff'
          period={14} animation={this.animation} upperLine={this.upperline} lowerLine={this.lowerline}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Exponential Moving Average (EMA)

Moving average Indicators are used to define the direction of the trend. To render a EMA Indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as `Ema` and
inject `EmaIndicator` into services.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject, StripLineDirective, StripLine, StripLinesDirective,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, ChartTheme,
    Crosshair, LineSeries, EmaIndicator, IndicatorsDirective, IndicatorDirective,AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, EmaIndicator]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Ema' field='Close' seriesName='Apple Inc' fill='#606eff' period={14} animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Momentum

Momentum shows the speed at which the price of the stock is changing. To render a Momentum indicator, use indicator
[`type`](../api/chart/technicalIndicatorModel/#type) as `Momentum`and inject `MomentumIndicator` module into services.
 Momentum indicator will be represented by two lines (upperLine,
signalLine).In momentum indicator the upperBand value is always renders at the value 100.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLinesDirective, StripLineDirective,
    Crosshair, LineSeries, MomentumIndicator, StripLine, ChartTheme, IndicatorsDirective, IndicatorDirective,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };
  public upperline = { color: '#e74c3d' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, MomentumIndicator, StripLine]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true} majorGridLines={this.lines} majorTickLines={this.lines} minimum={80} maximum={120} interval={20} title='Momentum' plotOffset={30} lineStyle={this.lines}>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Momentum' field='Close' seriesName='Apple Inc' yAxisName='secondary' fill='#6063ff'
          period={3} animation={this.animation} upperLine={this.upperline}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customization of MomentumIndicator**

`stroke`, `stroke-width`, and `color` of upperLine can be customized by using [`upperLine`](../api/chart/technicalIndicatorModel/#upperline)
property of indicator.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLinesDirective, StripLineDirective,
    Crosshair, LineSeries, MomentumIndicator, StripLine, ChartTheme, IndicatorsDirective, IndicatorDirective,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };
  public upperline = { color: '#e74c3d' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, MomentumIndicator, StripLine]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true} majorGridLines={this.lines} majorTickLines={this.lines} minimum={80} maximum={120} interval={20} title='Momentum' plotOffset={30} lineStyle={this.lines}>

        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Momentum' field='Close' seriesName='Apple Inc' yAxisName='secondary' fill='#6063ff'
          period={3} animation={this.animation} upperLine={this.upperline}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Moving Average Convergence Divergence (MACD)

MACD is based on the difference between two EMA's. To render a MACD Indicator, use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as
`Macd` and inject `MacdIndicator` module using into services. MACD indicator will be represented
by MACD line,signal line, MACD histogram. MACD histogram is used to differentiate MACD line and signal line.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLinesDirective, StripLineDirective,
    Crosshair, LineSeries, StripLine, MacdIndicator, ColumnSeries, ChartTheme, IndicatorsDirective, IndicatorDirective,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, MacdIndicator, StripLine, ColumnSeries]} />
      <AxesDirective>
        <AxisDirective opposedPosition={true} rowIndex={0} name='secondary'
          majorGridLines={this.lines} lineStyle={this.lines} minimum={-3.5} maximum={3.5} interval={3.5}
          majorTickLines={this.lines} title='MACD'>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Macd' period={3} fastPeriod={8} slowPeriod={5} seriesName='Apple Inc' macdType='Both' width={2} macdPositiveColor='#2ecd71' macdNegativeColor='#e74c3d' fill='#6063ff' yAxisName='secondary'>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customization of MACD**

`stroke`, `stroke-width`, and `color`of macdLine can be customized by using,[`macdLine`](../api/chart/technicalIndicatorModel/#macdline),
property of indicator. The positive and negative changes of histogram can be customized by [`macdPositiveColor`](../api/chart/technicalIndicatorModel/#macdpositivecolor)
and [`macdNegativeColor`](../api/chart/technicalIndicatorModel/#macdnegativecolor) properties. The [`macdType`] is used to define the type of
MACD indicator. To customize the MACD period using [`slowPeriod`](../api/chart/technicalIndicatorModel/#slowperiod) and [`fastPeriod`](../api/chart/technicalIndicatorModel/#fastperiod)
properties.

By default `macdType` as 'Both'.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLinesDirective, StripLineDirective,
    Crosshair, LineSeries, StripLine, MacdIndicator, ColumnSeries, ChartTheme, IndicatorsDirective, IndicatorDirective,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, MacdIndicator, StripLine, ColumnSeries]} />
      <AxesDirective>
        <AxisDirective opposedPosition={true} rowIndex={0} name='secondary'
          majorGridLines={this.lines} lineStyle={this.lines} minimum={-3.5} maximum={3.5} interval={3.5}
          majorTickLines={this.lines} title='MACD'>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d'
          type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Macd' period={3} fastPeriod={8} slowPeriod={5} seriesName='Apple Inc' macdType='Both' width={2} macdPositiveColor='#2ecd71' macdNegativeColor='#e74c3d' fill='#6063ff' yAxisName='secondary'>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Relative Strength Index (RSI)

RSI shows how strongly a stock is moving in its current direction. To render a RSI Indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as
`Rsi` and inject `RsiIndicator` module into services. RSI indicator will be represented
by three lines (upperBand, lowerBand, signalLine). The upperBand and lowerBand values are customized by
[`overBought`](../api/chart/technicalIndicatorModel/#overbought) and [`overSold`](../api/chart/technicalIndicatorModel/#oversold)
properties of indicator and the signalLine is calculated by RSI formula.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective,
    SeriesDirective, Inject, ILoadedEventArgs, StripLinesDirective, StripLineDirective,
    LineSeries, RsiIndicator, IndicatorsDirective, ChartTheme,
    IndicatorDirective, Category, StripLine, CandleSeries, Tooltip, DateTime, Zoom, Logarithmic, Crosshair,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };
  public upperline = { color: '#e74c3d' };
  public lowerline = { color: '#2ecd71' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, RsiIndicator, StripLine]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true} majorGridLines={this.lines}
          majorTickLines={this.lines} minimum={0} maximum={120} interval={60} title='RSI' lineStyle={this.lines}>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} xName='x' yName='silver' name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' low='low' open='open' close='close' high='high' volume='volume' type='Candle'>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective field='Close' yAxisName='secondary' type='Rsi' fill='#6063ff' seriesName='Apple Inc' period={3}
          showZones={true} overBought={70} overSold={30} upperLine={this.upperline} lowerLine={this.lowerline}
          animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Simple Moving Average (SMA)

Moving average Indicators are used to define the direction of the trend. To render a SMA Indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as
`Sma` and inject `SmaIndicator` module into services.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject, Legend, DateTime, Logarithmic, Tooltip, CandleSeries, DataLabel, Crosshair, Zoom, ColumnSeries, ILoadedEventArgs,
    LineSeries, SmaIndicator, IndicatorsDirective, IndicatorDirective, ChartTheme, StripLineDirective, StripLine, StripLinesDirective,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = {
    title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30,
    lineStyle: { width: 0 }
  };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, SmaIndicator]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='silver' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Sma' fill='blue' seriesName='Apple Inc' period={14}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Stochastic

It shows how a stock is, when compared to previous state. To render a Stochastic indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as `Stochastic`
and inject `StochasticIndicator` module into services.
stochastic indicator will be represented by four lines (upperLine, lowerLine, periodLine, signalLine).
In stochastic indicator the upperBand value and lowerBand value is customized by [`overBought`](../api/chart/technicalIndicatorModel/#overbought) and [`overSold`](../api/chart/technicalIndicatorModel/#oversold)
properties of indicators and the periodLine and signalLine is render based on stochastic formula.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    StripLine, DateTime, Logarithmic, Tooltip, CandleSeries, Crosshair, Zoom, ILoadedEventArgs, StripLinesDirective, StripLineDirective,
    LineSeries, StochasticIndicator, IndicatorsDirective, IndicatorDirective, Category, ChartTheme,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };
  public animation1 = { enable: false }
  public upperline = { color: '#e74c3d' };
  public lowerline = { color: '#2ecd71' };
  public periodline = { color: '#f2ec2f' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, StochasticIndicator]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true}
          majorGridLines={this.lines} majorTickLines={this.lines}
          minimum={0} maximum={120} interval={60} title='Stochastic' lineStyle={this.lines}>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Stochastic' field='Close' seriesName='Apple Inc' yAxisName='secondary' fill='#6063ff' kPeriod={2} dPeriod={3} showZones={true} periodLine={this.periodline} period={3} animation={this.animation1} upperLine={this.upperline} lowerLine={this.lowerline}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customization of StochasticIndicator**

`stroke`, `stroke-width`, and `color` of upperLine can be customized by using,[`upperLine`](../api/chart/technicalIndicatorModel/#upperline),
the lowerLine can be customized by using [`lowerLine`](../api/chart/technicalIndicatorModel/#lowerline) and the periodLine can be customized
by using [`periodLine`](../api/chart/technicalIndicatorModel/#periodline) properties of indicator. To customize the period to find the
average price using [`kPeriod`](../api/chart/technicalIndicatorModel/#kperiod) and [`dPeriod`](../api/chart/technicalIndicatorModel/#dperiod)
properties.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    StripLine, DateTime, Logarithmic, Tooltip, CandleSeries, Crosshair, Zoom, ILoadedEventArgs, StripLinesDirective, StripLineDirective,
    LineSeries, StochasticIndicator, IndicatorsDirective, IndicatorDirective, Category, ChartTheme,
    AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };
  public animation1 = { enable: false }
  public upperline = { color: '#e74c3d' };
  public lowerline = { color: '#2ecd71' };
  public periodline = { color: '#f2ec2f' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, StochasticIndicator]} />
      <RowsDirective>
        <RowDirective height={'40%'}></RowDirective>
        <RowDirective height={'60%'}></RowDirective>
      </RowsDirective>
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true}
          majorGridLines={this.lines} majorTickLines={this.lines}
          minimum={0} maximum={120} interval={60} title='Stochastic' lineStyle={this.lines}>
          <StripLinesDirective>
            <StripLineDirective start={0} end={120} text='' color='black' visible={true} opacity={0.03} zIndex='Behind'>
            </StripLineDirective>
          </StripLinesDirective>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Stochastic' field='Close' seriesName='Apple Inc' yAxisName='secondary' fill='#6063ff' kPeriod={2} dPeriod={3} showZones={true} periodLine={this.periodline} period={3} animation={this.animation1} upperLine={this.upperline} lowerLine={this.lowerline}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Triangular Moving Average (TMA)

Moving average Indicators are used to define the direction of the trend. To render a TMA Indicator,
use indicator [`type`](../api/chart/technicalIndicatorModel/#type) as
`Tma` and inject `TmaIndicator` module into services.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, CandleSeries, Category, Tooltip, DateTime,
    Zoom, Logarithmic, Crosshair, LineSeries, TmaIndicator, IndicatorsDirective, IndicatorDirective, ILoadedEventArgs,
    ChartTheme,AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public animation1 = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, DateTime, Logarithmic, Crosshair, LineSeries, TmaIndicator]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2} xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open' name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation1}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Tma' field='Close' seriesName='Apple Inc' fill='#6063ff' period={14} animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customization of Technical Indicators**

`stroke`, `stroke-width`, and `color` of signalLine can be customized by using,[`fill`](../api/chart/technicalIndicatorModel/#fill),
[`width`](../api/chart/technicalIndicatorModel/#width) and [`dashArray`](../api/chart/technicalIndicatorModel/#dasharray) properties.
and the [`period`](../api/chart/technicalIndicatorModel/#period) property is used to predict the data forecast
calculations. The [`field`](../api/chart/technicalIndicatorModel/#field) value is used to the compare the current price
with previous price. It is applicable to Bollinger bands and moving averages. The [`showZones`](../api/chart/technicalIndicatorModel/#showzones)
property is used to shows/Hides the overBought and overSold regions. It is applicable for RSI and stochastic indicators.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {
    ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, CandleSeries, Category, Tooltip, DateTime,
    Zoom, Logarithmic, Crosshair, LineSeries, TmaIndicator, IndicatorsDirective, IndicatorDirective, ILoadedEventArgs,
    ChartTheme,AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public animation1 = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, DateTime, Logarithmic, Crosshair, LineSeries, TmaIndicator]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2} xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open' name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation1}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='Tma' field='Close' seriesName='Apple Inc' fill='red' period={3} animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Data Source**

Usually technical indicators are added along with a financial series. The [`seriesName`](../api/chart/technicalIndicatorModel/#seriesname)
represents the series, the data of which has to be analysed through indicators.

Technical indicators can also be added without series using [`dataSource`](../api/chart/technicalIndicatorModel/#datasource) property of indicator.

{% tab template= "chart/series/technical-indicators",  isDefaultActive=true,  sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Browser } from '@syncfusion/ej2-base';
import {ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, RowDirective, RowsDirective, SeriesDirective, Inject,
    CandleSeries, Category, Tooltip, ILoadedEventArgs, DateTime, Zoom, Logarithmic, StripLineDirective,
    Crosshair, LineSeries, AccumulationDistributionIndicator, IAxisLabelRenderEventArgs,
    StripLine, ChartTheme, IndicatorsDirective, IndicatorDirective, StripLinesDirective,AxisModel,ChartAreaModel,CrosshairSettingsModel, TooltipSettingsModel}
from'@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public axisLableRender = (args: IAxisLabelRenderEventArgs): void => {
    if (args.axis.name === 'secondary') {
      let value: number = Number(args.text) / 1000000000;
      args.text = String(value) + 'bn';
    }
  }
  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Months', majorGridLines: { width: 0 }, crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { title: 'Price', labelFormat: '${value}', minimum: 30, maximum: 180, interval: 30, lineStyle: { width: 0 } };
  public animation = { enable: true };
  public chartarea: ChartAreaModel = { border: { width: 0 } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      crosshair={this.crosshair}
      axisLabelRender={this.axisLableRender.bind(this)}
      chartArea={this.chartarea}
      width={Browser.isDevice ? '100%' : '80%'}
      title='AAPL 2012-2017'>
      <Inject services={[CandleSeries, Category, Tooltip, StripLine, DateTime, Logarithmic, Crosshair, LineSeries, AccumulationDistributionIndicator]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='secondary' opposedPosition={true}
          majorGridLines={this.lines} majorTickLines={this.lines} minimum={-7000000000} maximum={5000000000}
          interval={6000000000} title='Accumulation Distribution' lineStyle={this.lines}>
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} width={2}
          xName='x' yName='y' low='low' high='high' close='close' volume='volume' open='open'
          name='Apple Inc' bearFillColor='#2ecd71' bullFillColor='#e74c3d' type='Candle' animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
      <IndicatorsDirective>
        <IndicatorDirective type='AccumulationDistribution' field='Close' seriesName='Apple Inc' yAxisName='secondary' fill='#6063ff' period={3} animation={this.animation}>
        </IndicatorDirective>
      </IndicatorsDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Module Dependencies**
To render a Indicator, it is mandatory to inject `LineSeries` module using `Chart.Inject(LineSeries)`.
In addition to that, MACD Indicator requires `ColumnSeries` and BollingerBands requires `RangeAreaSeries`.
