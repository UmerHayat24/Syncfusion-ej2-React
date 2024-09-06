---
title: " Stock Chart Appearance | React "

component: "StockChart"

description: "We can customize stock chart appearance by using title and tooltip customizations."
---

# Appearance

## Stock Chart Title

Stock Chart can be given a title using [`title`](../api/stock-chart/stockChartModel/#title) property, to show the information about the data plotted.

{% tab template="stock-chart/appearance/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,FontModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryxAxis: AxisModel= {
            valueType: 'DateTime',
            majorGridLines: { width: 0 },
            majorTickLines: { color: 'transparent' },
            crosshairTooltip: { enable: true }
    };
    public primaryyAxis: AxisModel= {
            labelFormat: 'n0',
            lineStyle: { width: 0 },
            rangePadding: 'None',
            majorTickLines: { width: 0 }
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public titlestyle:FontModel ={fontFamily: "Arial", color: '#424242 '};

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    tooltip={this.tooltip}
                    crosshair={this.crosshair}
                    height='350'
                    title='AAPL Stock Price'
                    titleStyle = { this.titlestyle }>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,       AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData}  type='Candle' animation={{ enable: true }}>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**Title Customization**

The `textStyle` property of chart title provides options to customize the `size`, `color`, `fontFamily`, `fontWeight`,`fontStyle`, `opacity`, `textAlignment` and `textOverflow`.

{% tab template="stock-chart/appearance/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,FontModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryxAxis: AxisModel= {
            valueType: 'DateTime',
            majorGridLines: { width: 0 },
            majorTickLines: { color: 'transparent' }
    };
    public primaryyAxis: AxisModel= {
            labelFormat: 'n0',
            majorTickLines: { width: 0 }
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public titlestyle:FontModel ={fontFamily: "Arial", color: '#424242 ',textOverflow: 'Wrap'};

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    title='AAPL Stock Price'
                    height='350'
                    titleStyle = { this.titlestyle }>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,       AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData}  type='Candle' animation={{ enable: true }}>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Stock Chart Theme

Changing Stock Chart theme will affect background color, grid lines, tooltip colors and appearance.

[`theme`](../api/stock-chart/stockChartModel/#theme) property of Stock chart is shipped with several built-in themes such as `Material`, `Fabric`, `Bootstrap` , `HighContrastLight`, `MaterialDark`, `FabricDark`, `FabricDark`, `HighContrast` and `BootstrapDark`.

{% tab template="stock-chart/appearance/theme", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,FontModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryxAxis: AxisModel= {
            valueType: 'DateTime',
            majorGridLines: { width: 0 },
            majorTickLines: { color: 'transparent' }
    };
    public primaryyAxis: AxisModel= {
            labelFormat: 'n0',
            majorTickLines: { width: 0 }
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    title='AAPL Stock Price'
                    height='350'
                    theme='HighContrast'>
                     <Inject services={[DateTime, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,       AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData}  type='Candle' animation={{ enable: true }}>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## See Also

* [Axis Customization](./axis-customization/)