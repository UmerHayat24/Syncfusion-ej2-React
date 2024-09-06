---
title: " Stock Chart Axis Customization | React "

component: "Stock Chart"

description: " Stock Chart axis contains different customization and types like axis crossing, multiple axis, inversed axis, tick and grid, title customizations"
---

# Axis Customization

## Axis Crossing

An axis can be positioned in the Stock Chart area using [`crossesAt`](../api/stock-chart/stockChartAxisModel/#crossesat) and [`crossesInAxis`] (../api/stock-chart/stockChartAxisModel/#crossesinaxis) properties. The [`crossesAt`] (../api/stock-chart/stockChartAxisModel/#crossesat) property specifies the values (datetime, numeric, or logarithmic) at which the axis line has to be intersected with the vertical axis or vice-versa, and the [`crossesInAxis`] (../api/stock-chart/stockChartAxisModel/#crossesinaxis) property specifies the axis name with which the axis line has to be crossed.

{% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                    crossesAt: 115
                }}
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' >
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Title

You can add a title to the axis using [`title`](../api/stock-chart/stockChartAxisModel/#title) property to provide quick
information to the user about the data plotted in the axis. Title style can be customized using [`titleStyle`](../api/stock-chart/stockChartAxisModel/#titlestyle) property of the axis.

{% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                    title: 'AAPL Historical',
                }}
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' >
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Tick Lines Customization

You can customize the  `width`, `color` and `size` of the minor and major tick lines, using
[`majorTickLines`](../api/stock-chart/stockChartAxisModel/#majorticklines) and
[`minorTickLines`](../api/stock-chart/stockChartAxisModel/#minorticklines) properties in the axis.

{% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

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

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
            majorTickLines : { color : 'blue', width : 5 },
            minorTickLines : {color : 'red',width : 0 }
    };
    public primaryYAxis: AxisModel= {
            majorTickLines : { color : 'green', width : 5 },
            minorTickLines : {color : 'red',width : 0 }
    };

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={ this.primaryXAxis }
                primaryYAxis={ this.primaryYAxis }
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' >
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Grid Lines Customization

You can customize the `width`, `color` and `dashArray` of the minor and major grid lines, using [`majorGridLines`](../api/stock-chart/stockChartAxisModel/#majorgridlines)
and [`minorGridLines`](../api/stock-chart/stockChartAxisModel/#minorgridlines) properties in the axis.

{% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

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

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
            majorGridLines : { color : 'blue', width : 5 },
            minorGridLines : {color : 'red',width : 0 }
    };
    public primaryYAxis: AxisModel= {
            majorGridLines : { color : 'green', width : 5 },
            minorGridLines : {color : 'red',width : 0 }
    };

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={ this.primaryXAxis }
                primaryYAxis={ this.primaryYAxis }
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' >
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Multiple Axis

In addition to primary X and Y axis, we can add n number of axis to the Stock Chart. Series can be associated with
this [`axis`](../api/stock-chart/stockChartAxisModel/) , by mapping with axis's unique name.

{% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel } from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines, Tooltip, AxesDirective, AxisDirective } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export,
StockChartAxesDirective, StockChartAxisDirective } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryxAxis: AxisModel= {
            valueType: 'DateTime',
            majorGridLines: { width: 0 }
    };
    public primaryyAxis: AxisModel= {
           majorTickLines: { width: 0 }
    };

    render(){
            return( <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    title='Multiple Axis'
                    height='350'>
                     <Inject services={[DateTime, RangeTooltip, Tooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartAxesDirective>
                        <StockChartAxisDirective rowIndex={0} name='yAxis1'>
                        </StockChartAxisDirective>
                      </StockChartAxesDirective>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Line' xName='date' yName='high' animation={{ enable: true }}>
                            </StockChartSeriesDirective>
                             <StockChartSeriesDirective dataSource={chartData} yAxisName='yAxis1' type='Line' animation={{ enable: true }} xName='date' yName='low'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
            );
      }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Inversed Axis

When an axis is inversed, highest value of the axis comes closer to origin and vice versa. To place an axis in inversed manner set this property
 [`isInversed`](../api/stock-chart/stockChartAxisModel/#isinversed) to true.

 {% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel } from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, RangeTooltip, Tooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
            isInversed: true
    };
    public primaryYAxis: AxisModel= {
            isInversed: true
    };

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={ this.primaryXAxis }
                primaryYAxis={ this.primaryYAxis }
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' >
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Opposed Position

To place an axis opposite from its original position, set
[`opposedPosition`](../api/stock-chart/stockChartAxisModel/#opposedposition) property of the axis to true.

{% tab template="stock-chart/axis-customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel } from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, RangeTooltip, Tooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
            opposedPosition: true
    };
    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={ this.primaryXAxis }
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle' >
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}
