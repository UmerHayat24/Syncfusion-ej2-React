---
title: " Stock Chart Appearance | React "

component: "StockChart"

description: "We can set chart size manually by using width and height properties. We can set percentage or pixel size values to the chart."
---

# Stock Chart Dimensions

## Size for Container

Stock Chart can render to its container size. You can set the size via inline or CSS as demonstrated below.

```html
 <div id="stockcharts" style="width:650px; height:350px"></div>
```

{% tab compileJsx=true%}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { StockChartComponent}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

  render(){
        return <StockChartComponent id='stockcharts'>
        </StockChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("stockcharts"));
```

{% endtab %}

{% tab template="stock-chart/chart-dimensions", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                title= 'Sales Analysis'
                bearFillColor='#2ecd71'
                bullFillColor='#e74c3d'
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' animation={{ enable: true }}>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Size for Stock Chart

You can also set size for stock chart directly through [`width`](../api/stock-chart/stockChartModel/#width) and [`height`](../api/stock-chart/stockChartModel/#height) properties.

<!-- markdownlint-disable MD036 -->
**In Pixel**
<!-- markdownlint-disable MD036 -->

You can set the size of chart in pixel as demonstrated below.

{% tab template="stock-chart/chart-dimensions", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                title= 'Sales Analysis'
                height='350'
                width='650'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' animation={{ enable: true }}>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**In Percentage**

By setting value in percentage, Stock Chart gets its dimension with respect to its container. For example, when
the height is ‘50%’, Stock Chart renders to half of the container height.

{% tab template="stock-chart/chart-dimensions", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                title= 'Sales Analysis'
                height='90%'
                width='80%'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' animation={{ enable: true }}>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: When you do not specify the size, it takes `450px` as the height and window size as its width.