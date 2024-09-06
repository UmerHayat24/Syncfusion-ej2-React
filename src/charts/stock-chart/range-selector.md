---
title: " StockChart Selecting Range | React "

component: "StockChart"

description: "we can able to select the particular range data by dragging thumbs or by tapping on the labels or by setting the start and end value properties. "
---

# Selecting Range

The left and right thumb of RangeNavigator are used to indicate the selected range in the large collection of data. Following are the ways you can select a range.

* By dragging the thumbs.
* By tapping on the labels.
* By setting the start and end through Date Range button.

Following code example shows the [`enableSelector`](../api/stock-chart/stockChartModel/#enableselector) property allows users to toggle the visibility of range selector.

{% tab template="stock-chart/range-selector", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
            majorTickLines: { width: 0 },
            crosshairTooltip: { enable: true }
    };
    public crosshair: CrosshairSettingsModel ={ enable: true } ;

    render(){
            return <StockChartComponent id='stockcharts'
                    enableSelector={false}
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    crosshair={this.crosshair}
                    height='350'
                    title='AAPL Stock Price'>
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