---
title: " Chart Other Types | React "

component: "Chart"

description: "Chart contains box and wishker, errorbar, waterfall and histogram charts and also supports different customization"
---
<!-- markdownlint-disable MD036 -->

# Box and whisker

To render a box and whisker chart, use series[`type`](../api/chart/seriesModel/#type) as `BoxAndWhisker` and inject
`BoxAndWhiskerSeries` services. The field y requires n number of data or it should contains minimum of five values to plot a segment.

{% tab template="chart/series/box", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         BoxAndWhiskerSeries, Category}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Development', y: [22, 22, 23, 25, 25, 25, 26, 27, 27, 28, 28, 29, 30, 32, 34, 32, 34, 36, 35, 38] },
    { x: 'Testing', y: [22, 33, 23, 25, 26, 28, 29, 30, 34, 33, 32, 31, 50] },
    { x: 'HR', y: [22, 24, 25, 30, 32, 34, 36, 38, 39, 41, 35, 36, 40, 56] },
    { x: 'Finance', y: [26, 27, 28, 30, 32, 34, 35, 37, 35, 37, 45] },
    { x: 'R&D', y: [26, 27, 29, 32, 34, 35, 36, 37, 38, 39, 41, 43, 58] },
    { x: 'Sales', y: [27, 26, 28, 29, 29, 29, 32, 35, 32, 38, 53] },
    { x: 'Inventory', y: [21, 23, 24, 25, 26, 27, 28, 30, 34, 36, 38] },
    { x: 'Graphics', y: [26, 28, 29, 30, 32, 33, 35, 36, 52] },
    { x: 'Training', y: [28, 29, 30, 31, 32, 34, 35, 36] }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', majorGridLines: { width: 0 }, };
  public primaryyAxis: AxisModel = { minimum: 10, maximum: 60, interval: 10, majorGridLines: { width: 0 }, majorTickLines: { width: 0 } };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryxAxis}
      title='Employee Age Group in Various Department'>
      <Inject services={[Category, BoxAndWhiskerSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' type='BoxAndWhisker' name='Department'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Customization of Box and Whisker series

### boxPlotMode

You can change the rendering mode of the Box and Whisker series using the `boxPlotMode` property.
The default boxPlotMode is `exclusive`.The other boxPlotMode available are `inclusive` and `normal`.

{% tab template="chart/series/box", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         BoxAndWhiskerSeries, Category}
from'@syncfusion/ej2-react-charts';
import { boxData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 10, maximum: 60, interval: 10 };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Employee Age Group in Various Department'>
      <Inject services={[Category, BoxAndWhiskerSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={boxData} xName='x' yName='y' type='BoxAndWhisker' name='Department'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

### showMean

In Box and Whisker series  `showMean` property is used to show the box and whisker average value. The default value of `showMedian` is false.

{% tab template="chart/series/box", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         BoxAndWhiskerSeries, Category}
from'@syncfusion/ej2-react-charts';
import { boxData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', majorGridLines: { width: 0 }, };
  public primaryyAxis: AxisModel = { minimum: 10, maximum: 60, interval: 10, majorGridLines: { width: 0 }, majorTickLines: { width: 0 } };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Employee Age Group in Various Department'>
      <Inject services={[Category, BoxAndWhiskerSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={boxData} xName='x' yName='y' type='BoxAndWhisker' name='Department' boxPlotMode='Normal'
          marker={this.marker} showMean='false'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Waterfall chart

To render a waterfall series, use series [`type`](../api/chart/seriesModel/#type) as `Waterfall`
and inject `WaterfallSeries` module into the `services`.

{% tab template="chart/series/waterfall", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, WaterfallSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: object[] = [
    { x: 'Income', y: 4711 }, { x: 'Sales', y: -1015 },
    { x: 'Development', y: -688 },
    { x: 'Revenue', y: 1030 }, { x: 'Balance' },
    { x: 'Expense', y: -361 }, { x: 'Tax', y: -695 },
    { x: 'Net Profit' }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', majorGridLines: { width: 0 }, plotOffset: 20 };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 5000, interval: 1000, majorGridLines: { width: 0 }, title: 'Expenditure' };
  public marker = { dataLabel: { visible: true, font: { color: '#ffffff' } } };
  public connector = { color: '#5F6A6A', width: 2 };
  public tooltip: TooltipSettingsModel = { enable: true, shared: false };
  public legendSettings: LegendSettingsModel = { visible: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      tooltip={this.tooltip}
      legendSettings={this.legendSettings}
      title='Company Revenue and Profit'>
      <Inject services={[WaterfallSeries, Category, Tooltip, Zoom, Crosshair, Legend, DataLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='USA' type='Waterfall' intermediateSumIndexes={[4]}
          sumIndexes={[7]} marker={this.marker} connector={this.connector} columnWidth={0.9}
          negativeFillColor='#e56590'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Customization of Waterfall Series**

The negative changes of waterfall series is
represented by using [`negativeFillColor`](../api/chart/seriesModel/#negativefillcolor) and the summary changes are
represented by using [`summaryFillColor`](../api/chart/seriesModel/#summaryfillcolor) properties.

By default, the negativeFillColor as ‘#E94649’ and the summaryFillColor as ‘#4E81BC’.

{% tab template="chart/series/waterfall", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, WaterfallSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { crossesAt: 15 };
  public primaryyAxis: AxisModel = { crossesAt: 5 };
  public marker = { dataLabel: { visible: true, font: { color: '#ffffff' } } };
  public connector = { color: '#5F6A6A', width: 2 };
  public tooltip: TooltipSettingsModel = { enable: true, shared: false };
  public legendSettings: LegendSettingsModel = { visible: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={{ valueType: 'Category', majorGridLines: { width: 0 }, plotOffset: 20 }}
      primaryYAxis={{ minimum: 0, maximum: 5000, interval: 1000, majorGridLines: { width: 0 }, title: 'Expenditure' }}
      tooltip={this.tooltip}
      legendSettings={this.legendSettings}
      title='Company Revenue and Profit'>
      <Inject services={[WaterfallSeries, Category, Tooltip, Zoom, Crosshair, Legend, DataLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='USA' type='Waterfall' intermediateSumIndexes={[4]}
          sumIndexes={[7]} marker={this.marker} connector={this.connector} columnWidth={0.9}
          summaryFillColor='#e56590' negativeFillColor='#f8b883'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Error Bar Chart

Error bars are graphical representations of the variability of data and used on graphs to indicate the error or uncertainty in a reported
measurement. To render the error bar for the series, set [`visible`](../api/chart/errorBarSettings/#visible)
as `true` and inject `ErrorBar` module into the `services`.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, ErrorBar }
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 2006, y: 7.8 }, { x: 2007, y: 7.2 },
    { x: 2008, y: 6.8 }, { x: 2009, y: 10.7 },
    { x: 2010, y: 10.8 }, { x: 2011, y: 9.8 }
  ];
  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = { minimum: 3, maximum: 12, interval: 1, title: 'Percentage', labelFormat: '{value}%' };
  public marker: { visible: true };
  public errorbar = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[LineSeries, Legend, Category, ErrorBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' width={2} name='India' type='Line'
          marker={this.marker} errorBar={this.errorbar}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Error Bar Type**

To change the error bar rendering type using [`type`](../api/chart/errorBarSettings/#type)
option of error bar. To change the error bar line length you can use [`verticalError`](../api/chart/errorBarSettings/#verticalerror)
property.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, ErrorBar }
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = { minimum: 3, maximum: 12, interval: 1, title: 'Percentage', labelFormat: '{value}%' };
  public marker: { visible: true };
  public errorbar = { visible: true, type: 'Percentage', verticalError: 4 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[LineSeries, Legend, Category, ErrorBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' width={2} name='India' type='Line'
          marker={this.marker} errorBar={this.errorbar}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Custom Error Bar**

To customize the error bar type, set error bar [`type`](../api/chart/errorBarSettings/#type) as `Custom` and
then change the horizontal/vertical positive and negative error of error bar.
.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, ErrorBar }
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = { minimum: 3, maximum: 12, interval: 1, title: 'Percentage', labelFormat: '{value}%' };
  public marker: { visible: true };
  public errorbar = {
    visible: true,
    type: 'Custom',
    mode: 'Both',
    verticalPostiveError: 3,
    horizontalPositiveError: 2,
    verticalNegativeError: 3,
    horizontalNegativeError: 2
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[LineSeries, Legend, Category, ErrorBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' width={2} name='India' type='Line'
          marker={this.marker} errorBar={this.errorbar}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Changing Error Bar Mode**

Error bar mode is used to define whether the error bar line has to be drawn horizontally, vertically or in both side.
To change the error bar mode use [`mode`](../api/chart/errorBarSettings/#mode) option.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, ErrorBar }
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = { minimum: 3, maximum: 12, interval: 1, title: 'Percentage', labelFormat: '{value}%' };
  public marker: { visible: true };
  public errorbar = { visible: true, mode: 'Horizontal' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[LineSeries, Legend, Category, ErrorBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' width={2} name='India' type='Line'
          marker={this.marker} errorBar={this.errorbar}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Changing Error Bar Direction**

To change the error bar direction to plus, minus or both side using [`direction`](../api/chart/errorBarSettings/#direction) option.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, ErrorBar }
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';
class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = { minimum: 3, maximum: 12, interval: 1, title: 'Percentage', labelFormat: '{value}%' };
  public marker: { visible: true };
  public errorbar = { visible: true, mode: 'Vertical', direction: 'Minus' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[LineSeries, Legend, Category, ErrorBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' width={2} name='India' type='Line'
          marker={this.marker} errorBar={this.errorbar}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

**Customizing Error Bar Cap**

To customize the error bar cap length, width and fill color, you can use [`errorBarCap`](../api/chart/errorBarSettings/#errorbarcap) option.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, ErrorBar }
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { minimum: 2005, maximum: 2012, interval: 1, title: 'Year' };
  public primaryyAxis: AxisModel = { minimum: 3, maximum: 12, interval: 1, title: 'Percentage', labelFormat: '{value}%' };
  public marker: { visible: true };
  public errorbar = {
    visible: true, errorBarCap: {
      length: 10,
      width: 10,
      color: '#0000ff'
    }
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Unemployment rate (%)'>
      <Inject services={[LineSeries, Legend, Category, ErrorBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' width={2} name='India' type='Line'
          marker={this.marker} errorBar={this.errorbar}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Vertical chart

In EJ2 chart, you can draw a chart in vertical manner by changing orientation of the axis. All series types support this feature.
You can use `isTransposed` property in chart to render a chart in vertical manner.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, SplineSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { splineData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public primaryxAxis: AxisModel= { title: 'Month',valueType: 'Category'}  ;
    public primaryyAxis: AxisModel= {  minimum: -5, maximum: 35, interval: 5,title: 'Temperature in Celsius',labelFormat: '{value}C'}  ;
    public marker:{ visible: true, width: 10, height: 10 };

    render(){
        return <ChartComponent id='charts'
                primaryXAxis={ this.primaryxAxis }
                primaryYAxis={ this.primaryyAxis }
                title='CO2 - Intensity Analysis' isTransposed={ true }>
                    <Inject services={[SplineSeries, Legend, Tooltip, DataLabel,  Category]}/>
                    <SeriesCollectionDirective>
                        <SeriesDirective dataSource ={splineData}  xName='x' yName='y' width={2} name='London' type='Spline'
                        marker={ this.marker }>
                        </SeriesDirective>
                    </SeriesCollectionDirective>
                </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Histogram Series

Histogram type charts can provide a visual display of large amounts of data that are difficult to understand in a tabular or spreadsheet form.
To render a histogram chart, use series [`type`](../api/chart/series/#type)  as `Histogram` and
inject `HistogramSeries`  module into the `services`.

{% tab template="chart/series/waterfall", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, ChartTheme,LegendSettingsModel,TooltipSettingsModel,
    Legend, Category, Tooltip, ColumnSeries, ILoadedEventArgs, DataLabel, HistogramSeries
} from '@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public chartData: Object[] = [];
    public points: number[] = [5.250, 7.750, 0, 8.275, 9.750, 7.750, 8.275, 6.250, 5.750,
        5.250, 23.000, 26.500, 27.750, 25.025, 26.500, 26.500, 28.025, 29.250, 26.750, 27.250,
        26.250, 25.250, 34.500, 25.625, 25.500, 26.625, 36.275, 36.250, 26.875, 40.000, 43.000,
        46.500, 47.750, 45.025, 56.500, 56.500, 58.025, 59.250, 56.750, 57.250,
        46.250, 55.250, 44.500, 45.525, 55.500, 46.625, 46.275, 56.250, 46.875, 43.000,
        46.250, 55.250, 44.500, 45.425, 55.500, 56.625, 46.275, 56.250, 46.875, 43.000,
        46.250, 55.250, 44.500, 45.425, 55.500, 46.625, 56.275, 46.250, 56.875, 41.000, 63.000,
        66.500, 67.750, 65.025, 66.500, 76.500, 78.025, 79.250, 76.750, 77.250,
        66.250, 75.250, 74.500, 65.625, 75.500, 76.625, 76.275, 66.250, 66.875, 80.000, 85.250,
        87.750, 89.000, 88.275, 89.750, 97.750, 98.275, 96.250, 95.750, 95.250
    ];
    public chartLoad(): void {
      this.points.map((value: number) => {
        this.chartData.push({
            y: value
            });
        });
    }
    public primaryxAxis: AxisModel= {  majorGridLines: { width: 0 }, title: 'Score of Final Examination',  minimum: 0, maximum: 100 }  ;
    public primaryyAxis: AxisModel= {   title: 'Number of Students', minimum: 0, maximum: 50, interval: 10, majorTickLines: { width: 0 }, lineStyle: { width: 0 }}  ;
    public legendSettings: LegendSettingsModel= { visible: false };
    public tooltipsettings: TooltipSettingsModel={ enable: true };
    public marker={ dataLabel: { visible: true, position: 'Top', font: { fontWeight: '600', color: '#ffffff' } } };

    render(){
        this.chartLoad();
        return <ChartComponent id='charts'
                primaryXAxis={ this.primaryxAxis }
                primaryYAxis={ this.primaryyAxis }
                tooltip={ this.tooltipsettings }
                legendSettings={ this.legendSettings }
                title='Examination Results'>
                    <Inject services={[HistogramSeries, Legend, Tooltip, Category, DataLabel]} />
                    <SeriesCollectionDirective>
                    <SeriesDirective dataSource={this.chartData}  yName='y' name='Score' type='Histogram'
                        marker={ this.marker }
                        showNormalDistribution={true} columnWidth={0.99} binInterval={20}>
                        </SeriesDirective>
                    </SeriesCollectionDirective>
              </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Pareto chart

Pareto charts are used to find the cumulative values of data in different categories. It is a combination of Column and Line series.
The initial values are represented by column chart and the cumulative values are represented by Line chart.
To render a pareto chart, use series [`type`](../api/chart/series/#type) as
`Pareto` and inject `ParetoSeries` `ColumnSeries` and  `LineSeries` module.

{% tab template="chart/series/waterfall", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, ChartTheme,LegendSettingsModel,TooltipSettingsModel,ParetoSeries,ColumnSeries,LineSeries,
    Legend, Category, Tooltip, ILoadedEventArgs, DataLabel
} from '@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public chartData: any[]=[
                    { x: 'Traffic', y: 56 }, { x: 'Child Care', y: 44.8 },
                    { x: 'Transport', y: 27.2 }, { x: 'Weather', y: 19.6 },
                    { x: 'Emergency', y: 6.6 }
                ];
    public primaryxAxis: AxisModel= {  title: 'Defects', valueType: 'Category' }  ;
    public primaryyAxis: AxisModel= {   title: 'Frequency', minimum: 0, maximum: 150,interval: 30 }  ;
    public tooltipsettings: TooltipSettingsModel={ enable: true };
    public marker={ visible: true, width: 10, height: 10};

    render(){
        return <ChartComponent id='charts'
                primaryXAxis={ this.primaryxAxis }
                primaryYAxis={ this.primaryyAxis }
                tooltip={ this.tooltipsettings }
                title='Defect vs Frequency'>
                    <Inject services={[ColumnSeries, LineSeries, ParetoSeries, Legend, Tooltip, Category, DataLabel]} />
                    <SeriesCollectionDirective>
                    <SeriesDirective dataSource={this.chartData}  xName='x' yName='y' name='Defect' type='Pareto'
                        marker={ this.marker }>
                        </SeriesDirective>
                    </SeriesCollectionDirective>
              </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## See Also

* [Data label](./data-labels/)
* [Tooltip](./tool-tip/)
