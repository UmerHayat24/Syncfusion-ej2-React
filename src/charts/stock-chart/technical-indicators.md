---
title: " StockChart Technical Indicators | React "

component: "StockChart"

description: "Indicators represent a statistical approach to technical analysis as opposed to a subjective approach. we have different types of indicators."
---
<!-- markdownlint-disable MD036 -->

# Technical Indicators

A technical indicator is a mathematical calculation based on historic price, volume or open interest information
that aims to forecast financial market direction.

StockChart supports 10 types of technical indicators namely `Accumulation Distribution`, `ATR`, `EMA`,`SMA`,`TMA`,`Momentum`,`MACD`,`RSI`,`Stochastic`,`Bollinger Band`. By using indicator dropdown box you can add an remove the required indicators types.

## Accumulation Distribution

Accumulation Distribution combines price and volume to show how money may be flowing into or out of stock.
To render a Accumulation Distribution Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `AccumulationDistribution` and inject
`AccumulationDistributionIndicator` module using `<Inject services={[AccumulationDistributionIndicator]}>`.
To calculate the signal line [`volume`](../api/stock-chart/stockChartIndicatorModel/#volume) field is additionally added with `dataSource`.

## Average True Range (ATR)

ATR measures the stock volatility by comparing the current value with the previous value.
To render a Average True Range (ATR) Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Atr` and inject `AtrIndicator` module using `<Inject services={[AtrIndicator]}>`.

## Exponential Moving Average (EMA)

Moving average Indicators are used to define the direction of the trend. To render a EMA Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Ema` and
inject `EmaIndicator` module using `<Inject services={[EmaIndicator}]>`.

## Momentum

Momentum shows the speed at which the price of the stock is changing. To render a Momentum indicator, use indicator
[`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Momentum`and inject `MomentumIndicator` module using
`<Inject services={[MomentumIndicator]}>` method. Momentum indicator will be represented by two lines (upperLine,
signalLine).In momentum indicator the upperBand value is always renders at the value 100.

## Moving Average Convergence Divergence (MACD)

MACD is based on the difference between two EMA's. To render a MACD Indicator, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`Macd` and inject `MacdIndicator` module using `<Inject services={[MacdIndicator]}>`.MACD indicator will be represented
by MACD line,signal line, MACD histogram. MACD histogram is used to differentiate MACD line and signal line.

## Relative Strength Index (RSI)

RSI shows how strongly a stock is moving in its current direction. To render a RSI Indicator, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`Rsi` and inject `RsiIndicator` module using `<Inject services={[Rsindicator]}>`.RSI indicator will be represented
by three lines (upperBand, lowerBand, signalLine). The upperBand and lowerBand values are customized by
[`overBought`](../api/stock-chart/stockChartIndicatorModel/#overbought) and [`overSold`](../api/stock-chart/stockChartIndicatorModel/#oversold)
properties of indicator and the signalLine is calculated by RSI formula.

## Simple Moving Average (SMA)

Moving average Indicators are used to define the direction of the trend. To render a SMA Indicator, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`Sma` and inject `SmaIndicator` module using `<Inject services={[SmaIndicator]}>`.

## Stochastic

It shows how a stock is, when compared to previous state. To render a Stochastic indicator, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Stochastic`
and inject `StochasticIndicator` module using `Chart.Inject(StochasticIndicator)` method.
stochastic indicator will be represented by four lines (upperLine, lowerLine, periodLine, signalLine).
In stochastic indicator the upperBand value and lowerBand value is customized by [`overBought`](../api/stock-chart/stockChartIndicatorModel/#overbought) and [`overSold`](../api/stock-chart/stockChartIndicatorModel/#oversold)
properties of indicators and the periodLine and signalLine is render based on stochastic formula.

## Triangular Moving Average (TMA)

Moving average Indicators are used to define the direction of the trend. To render a TMA Indicator, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`Tma` and inject `TmaIndicator` module using `<Inject services={[TmaIndicator]}>`.

## Bollinger Band

A StockChart overlay that shows the upper and lower limits of normal price movements based on the standard deviation of prices.
To render a Bollinger Band, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `BollingerBand`
and inject `BollingerBands` module using `<Inject services={[BollingerBands]}>` method.
Bollinger band will be represented by three lines (upperLine, lowerLine, signalLine).
The default values of the Bollinger Band [`period`](../api/stock-chart/stockChartIndicatorModel/#period) is 14 and [`standardDeviations`](../api/stock-chart/stockChartIndicatorModel/#standarddeviation) is 2.

{% tab template="stock-chart/technical-indicators", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject,
    DateTime, Tooltip, RangeTooltip, Crosshair, CandleSeries, Trendlines, StockChartIndicatorsDirective, StockChartIndicatorDirective, LineSeries, SplineSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries
} from '@syncfusion/ej2-react-charts';
import { BollingerBands } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {
        public upperline: Object = { color: '#ffb735', width: 1 };
        public lowerline: Object = { color: '#f2ec2f', width: 1 };
    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    majorGridLines: { color: 'transparent' }, crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    lineStyle: { color: 'transparent' },
                    majorTickLines: { color: 'transparent', width: 0 }
                }}
                crosshair={{ enable: true }}
                tooltip={{ enable: true }}
                seriesType={[]}
                exportType={[]}
                trendlineType={[]}
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, CandleSeries, BollingerBands,
                LineSeries, SplineSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' name='Apple Inc'
                    bearFillColor='#00226C' bullFillColor="#0450C2" fill='blue'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
                <StockChartIndicatorsDirective>
                    <StockChartIndicatorDirective type='BollingerBands' field='Close' seriesName='Apple Inc' fill='#606eff' xName='date' high='high' low='low' open='open' close='close' period={10} upperLine={this.upperline} lowerLine={this.lowerline}>
                    </StockChartIndicatorDirective>
                </StockChartIndicatorsDirective >
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}