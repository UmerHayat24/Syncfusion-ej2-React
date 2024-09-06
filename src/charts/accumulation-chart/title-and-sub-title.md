---
title: "Title and SubTitle | React "

component: "Accumulation Chart"

description: "Accumulation Chart title and sub title shows information about plotted data"
---

# Title

Accumulation Chart can be given a title using [`title`](../api/accumulation-chart/accumulationChartModel/#title) property, to show the information
about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 Inject,LegendSettingsModel}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

public data: any[] = [
        { x: 'Saudi Arabia', y: 58, text: '58%' },
        { x: 'Persian Gulf', y: 15, text: '15%' },
        { x: 'Canada', y: 13, text: '13%' },
        { x: 'Venezuela', y: 8, text: '8%' },
        { x: 'Mexico', y: 3, text: '3%' },
        { x: 'Russia', y: 2, text: '2%' },
        { x: 'Miscellaneous', y: 1, text: '1%' }];

  public legendSettings: LegendSettingsModel = { visible: true };

 render() {
    return <AccumulationChartComponent id='charts' legendSettings={this.legendSettings} title='Oil and other liquid imports in USA' legendSettings={{ visible: false }>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' dataLabel={{
                visible: true,
                name: 'text',
                font: {
                  fontWeight: '600'
                }
              }}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

# Title Customization

Accumulation Chart can be customizing a title using [`titleStyle`](../api/accumulation-chart/accumulationChartModel/#titlestyle) property.

{% tab template="chart/chart-title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 Inject,LegendSettingsModel}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

public data: any[] = [
        { x: 'Saudi Arabia', y: 58, text: '58%' },
        { x: 'Persian Gulf', y: 15, text: '15%' },
        { x: 'Canada', y: 13, text: '13%' },
        { x: 'Venezuela', y: 8, text: '8%' },
        { x: 'Mexico', y: 3, text: '3%' },
        { x: 'Russia', y: 2, text: '2%' },
        { x: 'Miscellaneous', y: 1, text: '1%' }];

  public legendSettings: LegendSettingsModel = { visible: true };
  public title: any = {
                          fontFamily: "Arial",
                          fontStyle: 'italic',
                          fontWeight: 'regular',
                          color: "#E27F2D",
                          size: '23px'
                         };

 render() {
    return <AccumulationChartComponent id='charts' legendSettings={this.legendSettings} title='Oil and other liquid imports in USA' subTitle ='In the year 2014 - 2015' legendSettings={{ visible: false }>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' titleStyle={this.title} dataLabel={{
                visible: true,
                name: 'text',
                font: {
                  fontWeight: '600'
                }
              }}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## SubTitle

Accumulation Chart can be given a subtitle using [`subTitle`](../api/accumulation-chart/accumulationChartModel/#subtitle) property, to show the information
about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 Inject,LegendSettingsModel}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

public data: any[] = [
        { x: 'Saudi Arabia', y: 58, text: '58%' },
        { x: 'Persian Gulf', y: 15, text: '15%' },
        { x: 'Canada', y: 13, text: '13%' },
        { x: 'Venezuela', y: 8, text: '8%' },
        { x: 'Mexico', y: 3, text: '3%' },
        { x: 'Russia', y: 2, text: '2%' },
        { x: 'Miscellaneous', y: 1, text: '1%' }];

  public legendSettings: LegendSettingsModel = { visible: true };

 render() {
    return <AccumulationChartComponent id='charts' legendSettings={this.legendSettings} title='Oil and other liquid imports in USA' subTitle ='In the year 2014 - 2015' legendSettings={{ visible: false }>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' dataLabel={{
                visible: true,
                name: 'text',
                font: {
                  fontWeight: '600'
                }
              }}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## SubTitle Customization

Accumulation Chart can be customizing a subtitle using [`subTitleStyle`](../api/accumulation-chart/accumulationChartModel/#subtitlestyle) property, to show the information
about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 Inject,LegendSettingsModel}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

public data: any[] = [
        { x: 'Saudi Arabia', y: 58, text: '58%' },
        { x: 'Persian Gulf', y: 15, text: '15%' },
        { x: 'Canada', y: 13, text: '13%' },
        { x: 'Venezuela', y: 8, text: '8%' },
        { x: 'Mexico', y: 3, text: '3%' },
        { x: 'Russia', y: 2, text: '2%' },
        { x: 'Miscellaneous', y: 1, text: '1%' }];

  public legendSettings: LegendSettingsModel = { visible: true };
  public subTitle: any = {
                          fontFamily: "Arial",
                          fontStyle: 'italic',
                          fontWeight: 'regular',
                          color: "#E27F2D",
                          size: '13px'
                         };

 render() {
    return <AccumulationChartComponent id='charts' legendSettings={this.legendSettings} title='Oil and other liquid imports in USA' subTitle ='In the year 2014 - 2015' legendSettings={{ visible: false }>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' subTitleStyle={this.subTitle} dataLabel={{
                visible: true,
                name: 'text',
                font: {
                  fontWeight: '600'
                }
              }}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}
