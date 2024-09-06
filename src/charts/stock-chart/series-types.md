---
title: " Series Types | React "

component: "StockChart"

description: "Essential JS 2 StockChart  StockChart supports 32 types of series and also supports different tpes customizations for each type of StockChart."
---

# StockChart Series Types

Essential JS 2 StockChart supports 6 major types of series namely `Line`, `Spline`, `Hilo`, `HiloOpenClose`, `Hollow Candle` and `Candle` . By using the series dropdown button you can navigate between the above listed series types.

<!-- markdownlint-disable MD036 -->

## Line

To render a line series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Line` and
inject `LineSeries` module using `<Inject services={[LineSeries]}>` method.

## Spline

To render a spline series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Spline` and
inject `SplineSeries` module using `<Inject services={[SplineSeries]}>` method.

## Hilo

To render a hilo series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Hilo` and
inject `HiloSeries` module using `<Inject services={[HiloSeries]}>` method.

## HiloOpenClose

To render a hiloOpenClose series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `HiloOpenClose` and
inject `HiloOpenCloseSeries` module using `<Inject services={[HiloOpenCloseSeries]}>` method.

## HollowCandle

To render a hollowcandle series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Candle` and set `enableSolidCandle` as false. Now inject `CandleSeries` module using `<Inject services={[CandleSeries]}>` method.

## Candle

To render a candle series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Candle` and
inject `CandleSeries` module using `<Inject services={[CandleSeries]}>` method.

{% tab template="stock-chart/series-types", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, ITooltipRenderEventArgs, IStockChartEventArgs, ChartTheme,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';
import {
    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator,
    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    valueType: 'DateTime',
                }}
                height='350'
                indicatorType={[]}
                trendlineType={[]}
                exportType={[]}
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}