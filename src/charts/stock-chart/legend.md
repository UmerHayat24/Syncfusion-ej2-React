---
title: " Stock Chart Legend | React "

component: "Stock Chart"

description: "Stock Chart legend provides information about the series rendered in the Stock Chart.It has different alignment, shapes and customization properties. "
---

# Legend

Legend provides information about the series rendered in the Stock Chart. Legend can be added to a Stock Chart by enabling the [`visible`](../api/stock-chart/legendSettings/#visible) option in the [`legendSettings`](../api/stock-chart/legendSettings/).

## Position and Alignment

By using the [`position`](../api/stock-chart/legendSettings/#position) property, legend can be placed at `Left`, `Right`, `Top`, `Bottom` or `Custom` of the Stock Chart. The legend is positioned at the bottom of the Stock Chart, by default.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true, position: 'Top' };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

[`Custom`](../api/stock-chart/legendSettings/#position) position is used to position the legend anywhere in the Stock Chart using x, y coordinates.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true, position:'Custom', location: { x: 200, y: 20 } };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**Legend Alignment**

<!-- markdownlint-disable MD036 -->

The legend can be align as `Center`, `Far` or `Near` to the Stock Chart using [`alignment`](../api/stock-chart/legendSettings/#alignment) property.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true, position:'Bottom', alignment: 'Near' };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customization

To change the legend icon shape, [`legendShape`](../api/stock-chart/stockSeries/#legendshape-string) property in the [`series`](../api/stock-chart/stockSeries/) can be used. By default legend icon shape is `seriesType`.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL' legendShape= 'Pentagon'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Legend Size**

By default, legend takes 20% - 25% of the Stock Chart's height horizontally, when it is placed on top or bottom position and 20% - 25% of the width vertically, while placing on left or right position of the Stock Chart. The default legend size can be changed by using the [`width`](../api/stock-chart/legendSettings/#width) and [`height`](../api/stock-chart/legendSettings/#height) property of the `legendSettings`.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true, width: '500', height: '50', border: { width: 1, color: 'pink'} };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Legend Item Size**

The size of the legend items can customized by using the [`shapeHeight`](../api/stock-chart/legendSettings/#shapeheight) and [`shapeWidth`](../api/stock-chart/legendSettings/#shapewidth) property.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true, shapeHeight: 15, shapeWidth: 15 };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Collapsing Legend Item

By default, series name will be displayed as legend. To skip the legend for a particular series, empty string to the series name can be given.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Legend Title

The title for legend can be set using [`title`](../api/stock-chart/legendSettings/#title) property in `legendSettings`. Customize the [`fontStyle`](../api/stock-chart/stockChartFont/#fontstyle), [`size`](../api/stock-chart/stockChartFont/#size), [`fontWeight`](../api/stock-chart/stockChartFont/#fontweight), [`color`](../api/stock-chart/stockChartFont/#color), [`textAlignment`](../api/stock-chart/stockChartFont/#textalignment), [`fontFamily`](../api/stock-chart/stockChartFont/#fontfamily), [`opacity`](../api/stock-chart/stockChartFont/#opacity) and [`textOverflow`](../api/stock-chart/stockChartFont/#textoverflow) of legend title. [`titlePosition`](../api/stock-chart/legendSettings/#titleposition) is used to set the legend position in `Top`, `Left` and `Right` position. [`maximumTitleWidth`](../api/stock-chart/legendSettings/#maximumtitlewidth) is used to set the width of the legend title. By default, it will be `100px`.

{% tab template="stock-chart/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, CrosshairSettingsModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines } from '@syncfusion/ej2-react-charts';
import { EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export, StockLegend } from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryXAxis: AxisModel= {
            valueType: 'DateTime',
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;
    public tooltip: TooltipSettingsModel ={ enable: true } ;
    public legendSettings: LegendSettingsModel = { visible: true, title: 'Countries', titlePosition: 'Top', titleStyle: { fontFamily: 'verdana', fontStyle: 'Normal', fontWeight: 'Normal', size: '15px', textAlignment: 'Center', color: 'blue', textOverflow: 'None' }, maximumTitleWidth: 150 };

    render(){
            return <StockChartComponent id='stockcharts'
                    primaryXAxis={ this.primaryXAxis }
                    crosshair={this.crosshair}
                    tooltip={this.tooltip}
                    legendSettings={this.legendSettings}
                    indicatorType={[]}
                    trendlineType ={[]}
                    height='350'
                    title='AAPL Stock Price'>
                     <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export, StockLegend, AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]}/>
                      <StockChartSeriesCollectionDirective>
                            <StockChartSeriesDirective dataSource={chartData} type='Candle' name='AAPL'>
                            </StockChartSeriesDirective>
                        </StockChartSeriesCollectionDirective>
                  </StockChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: To use legend feature, we need to inject `StockLegend` module into the `services`.