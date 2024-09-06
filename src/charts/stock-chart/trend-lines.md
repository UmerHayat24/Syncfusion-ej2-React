---
title: " StockChart Trendlines | React "

component: "StockChart"

description: "Trendlines are used to show the direction and speed of price. StockChart supports 6 types of trendlines and also provides trendlines customization."
---
<!-- markdownlint-disable MD036 -->

# Trendlines

Trendlines are used to show the direction and speed of price.

StockChart supports 6 types of trendlines namely `Linear`,`Exponential`,`Logarithmic`,`Polynomial`,`Power`,`Moving Average`. By using trendline dropdown button you can add or remove the required trendline type.

## Linear

A linear trendline is a best fit straight line that is used with simpler data sets. To render a linear trendline,
use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Linear` and inject
`Trendlines` module using `<Inject services={[Trendlines]}>`.

## Exponential

An exponential trendline is a curved line that is most useful when data values rise or fall at increasingly higher rates. You cannot create an exponential trendline, if your data contains zero or negative values.

To render a exponential trendline,
use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Exponential` and inject
`Trendlines` module using `<Inject services={[Trendlines]}>`.

## Logarithmic

A logarithmic trendline is a best-fit curved line that is most useful when the rate of change in the data increases or decreases quickly and then levels out. A logarithmic trendline can use negative and/or positive values.

To render a logarithmic trendline, use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Logarithmic` and inject
`Trendlines` module using `<Inject services={[Trendlines]}>`.

## Polynomial

A polynomial trendline is a curved line that is used when data fluctuates.

To render a polynomial trendline,
use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Polynomial` and inject
`Trendlines` module using `<Inject services={[Trendlines]}>`.

`polynomialOrder` used to define the polynomial value.

## Power

A power trendline is a curved line that is best used with data sets that compare measurements that increase at a specific rate.

To render a power trendline, use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Power` and inject
`Trendlines` module using `<Inject services={[Trendlines]}>`.

## Moving Average

A moving average trendline smoothen out fluctuations in data to show a pattern or trend more clearly.

To render a moving average trendline, use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `MovingAverage` and inject
`Trendlines` module using `<Inject services={[Trendlines]}>`.

`period` property defines the period to find the moving average.

{% tab template="stock-chart/trend-lines", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';

import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    title: 'Months'
                }}
                primaryYAxis={{
                    title: 'Rupees against Dollars',
                    interval: 5
                }}
                tooltip={{enable:true}}
                height='350'
                title='Historical Indian Rupee Rate (INR USD)'
                indicatorType={[]}
                exportType={[]}
                seriesType={[]}
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        );
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}