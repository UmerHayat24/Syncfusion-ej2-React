---
title: " Chart Legend | React "

component: "Chart"

description: "Chart legend provides information about the series rendered in the chart.It has different alignment, shapes and customization properties. "
---

# Legend

Legend provides information about the series rendered in the chart.

To get start quickly with Legends in React Charts, you can check on this video:

`youtube:7VYeN4W_wMc`

## Position and Alignment

By using the [`position`](../api/chart/legendSettings/#position) property, you can position the legend
at left, right, top or bottom of the chart. The legend is positioned at the bottom of the chart, by default.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, position: 'Top' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

Custom position helps you to position the legend anywhere in the chart using x, y coordinates.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = {
    visible: true, position: 'Custom',
    location: { x: 200, y: 40 }
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Legend Reverse

You can reverse the order of the legend items by using the [`reverse`](../api/chart/legendSettings/#reverse) property. By default, legend for the first series in the collection will be placed first.

{% tab template="chart/axis/legend-reverse", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  ChartComponent,
  SeriesCollectionDirective,
  SeriesDirective,
  Inject,
  Legend,
  Category,
  Tooltip,
  ColumnSeries,
  DataLabel }
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: 'USA', gold: 50, silver: 70, bronze: 45 },
    { country: 'China', gold: 40, silver: 60, bronze: 55 },
    { country: 'Japan', gold: 70, silver: 60, bronze: 50 },
    { country: 'Australia', gold: 60, silver: 56, bronze: 40 },
    { country: 'France', gold: 50, silver: 45, bronze: 35 },
    { country: 'Germany', gold: 40, silver: 30, bronze: 22 },
    { country: 'Italy', gold: 40, silver: 35, bronze: 37 },
    { country: 'Sweden', gold: 30, silver: 25, bronze: 27 },
  ];
  render() {
    return (
      <ChartComponent
        id="charts"
        primaryXAxis={{
          valueType: 'Category',
          interval: 1,
          majorGridLines: { width: 0 },
        }}
        primaryYAxis={{
          majorGridLines: { width: 0 },
          majorTickLines: { width: 0 },
          lineStyle: { width: 0 },
          labelStyle: { color: 'transparent' },
        }}
        title="Olympic Medals"
        legendSettings={{
            visible: true,
            reverse: true
        }}
      >
        <Inject
          services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]}
        />
        <SeriesCollectionDirective>
          <SeriesDirective
            dataSource={this.data}
            xName="country"
            yName="gold"
            name="Gold"
            type="Column"
          ></SeriesDirective>
          <SeriesDirective
            dataSource={this.data}
            xName="country"
            yName="silver"
            name="Silver"
            type="Column"
          ></SeriesDirective>
          <SeriesDirective
            dataSource={this.data}
            xName="country"
            yName="bronze"
            name="Bronze"
            type="Column"
          ></SeriesDirective>
        </SeriesCollectionDirective>
      </ChartComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**Legend Alignment**

<!-- markdownlint-disable MD036 -->

You can align the legend as `center`, `far` or `near` to the chart using
[`alignment`](../api/chart/legendSettings/#alignment) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { position: 'Top', alignment: 'Near' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customization

To change the legend icon shape, you can use [`legendShape`](../api/chart/series/#legendshape) property
in the [`series`](../api/chart/series/). By default legend icon shape is `seriesType`.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { position: 'Top' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          legendShape='Circle' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver'
          legendShape='SeriesType' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze'
          legendShape='Rectangle' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Legend Size

By default, legend takes 20% - 25% of the chart's height horizontally, when it is placed on top or bottom position and 20% - 25% of the
chart's width vertically, when placed on left or right position of the chart. You can change this default legend size by using the
[`width`](../api/chart/legendSettings/#width) and [`height`](../api/chart/legendSettings/#height) property of the `legendSettings`.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, height: '100', width: '500' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          legendShape='Circle' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver'
          legendShape='SeriesType' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze'
          legendShape='Rectangle' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Legend Item Size

You can customize the size of the legend items by using the [`shapeHeight`](../api/chart/legendSettings/#shapeheight)
and [`shapeWidth`](../api/chart/legendSettings/#shapewidth) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, shapeHeight: 12, shapeWidth: 12 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          legendShape='Circle' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver'
          legendShape='SeriesType' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze'
          legendShape='Rectangle' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Paging for Legend

Paging will be enabled by default, when the legend items exceeds the legend bounds. You can view each legend
items by navigating between the pages using navigation buttons.

{% tab template="chart/axis/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, LineSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'WW', y: 12, y1: 22, y2: 38.3, y3: 50 },
    { x: 'EU', y: 9.9, y1: 26, y2: 45.2, y3: 63.6 },
    { x: 'APAC', y: 4.4, y1: 9.3, y2: 18.2, y3: 20.9 },
    { x: 'LATAM', y: 6.4, y1: 28, y2: 46.7, y3: 65.1 },
    { x: 'MEA', y: 30, y1: 45.7, y2: 61.5, y3: 73 },
    { x: 'NA', y: 25.3, y1: 35.9, y2: 64, y3: 81.4 }
  ];
  public primaryxAxis: AxisModel = {
    title: 'Countries', valueType: 'Category', interval: 1,
    labelIntersectAction: 'Rotate45'
  };
  public primaryyAxis: AxisModel = {
    title: 'Penetration (%)', rangePadding: 'None', labelFormat: '{value}%',
    minimum: 0, maximum: 90
  };
  public legendSettings: LegendSettingsModel = {
    padding: 10, shapePadding: 10,
    visible: true, border: {
      width: 2, color: 'grey'
    },
    width: '200'
  };
  public marker1 = { visible: true, width: 10, height: 10, shape: 'Diamond' };
  public marker2 = { visible: true, width: 10, height: 10, shape: 'Pentagon' };
  public marker3 = { visible: true, width: 10, height: 10, shape: 'Triangle' };
  public marker4 = { visible: true, width: 10, height: 10, shape: 'Circle' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' type='Line' width={2}
          name='December 2007' marker={this.marker1} >
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' type='Line' width={2}
          name='December 2008' marker={this.marker2} >
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y2' type='Line' width={2}
          name='December 2009' marker={this.marker3} >
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y3' type='Line' width={2}
          name='December 2010' marker={this.marker4} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Legend Text Wrap

When the legend text exceeds the container, the text can be wrapped by using  [`textWrap`](../api/chart/legendSettings/#textwrap) Property. End user can also wrap the legend text based on the [`maximumLabelWidth`](../api/chart/legendSettings/#maximumlabelwidth) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, position: 'Right', textWrap:'Wrap', maximumLabelWidth:50, };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold Medals' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver Medals' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze Medals' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Set the label color based on series color

You can set the legend label color based on series color by using chart's [loaded](../api/chart/#loaded) event.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, Chart, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, ILoadedEventArgs}
from'@syncfusion/ej2-react-charts';

// declare the series colors
let colors: string[] = ['#00BDAE', '#404041', '#357CD2'];

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, position: 'Top' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      loaded={this.onChartLoaded.bind(this)}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

  onChartLoaded(args: ILoadedEventArgs) {
    let chart: Chart = document.getElementById('charts');
    let legendTextCol: HTMLElement = chart.querySelectorAll('[id*="chart_legend_text_"]');
    for (let i = 0; i < legendTextCol.length; i++) {
        //set the color to legend label
        legendTextCol[i].setAttribute('fill', colors[i]);
    }
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Series Selection on Legend

By default, legend click enables you to collapse the series visibility.  On other hand, if you need to select
a series through legend click, disable the
[`toggleVisibility`](../api/chart/legendSettings/#togglevisibility).

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, toggleVisibility: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      selectionMode='Series'
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, Selection]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          legendShape='Circle' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' name='Silver'
          legendShape='SeriesType' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze'
          legendShape='Rectangle' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
  ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Enable Animation

You can customize the animation while clicking legend by setting enableAnimation as true or false using `enableAnimation` property in chart.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,TooltipSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData1: any[] = [{ x: 'USA', y: 46 }, { x: 'GBR', y: 27 }, { x: 'CHN', y: 26 }];
  public chartData2: any[] = [{ x: 'USA', y: 37 }, { x: 'GBR', y: 23 }, { x: 'CHN', y: 18 }];
  public chartData3: any[] = [{ x: 'USA', y: 38 }, { x: 'GBR', y: 17 }, { x: 'CHN', y: 26 }];
  public primaryxAxis: AxisModel = {valueType: 'Category', interval: 1, majorGridLines: { width: 0 } };
  public primaryyAxis: AxisModel = {majorGridLines: { width: 0 },
            majorTickLines: { width: 0 }, lineStyle: { width: 0 }, labelStyle: { color: 'transparent'}};
  public marker = { dataLabel: { visible: true, position: 'Top', font: { fontWeight: '600', color: '#ffffff' } } };
  public tooltip: TooltipSettingsModel = { enable: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medal Counts - RIO'
      enableAnimation={true}
      tooltip={this.tooltip}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, Selection]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData1} xName='x' yName='y' name='Gold'
          marker={this.marker} type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.chartData2} xName='x' yName='y' name='Silver'
          marker={this.marker} type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.chartData3} xName='x' yName='y' name='Bronze'
          marker={this.marker} type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
  ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Collapsing Legend Item

By default, series name will be displayed as legend. To skip the legend for a particular series, you can give empty string to the series name.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public legendSettings: LegendSettingsModel = { visible: true, toggleVisibility: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          legendShape='Circle' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze'
          legendShape='Rectangle' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Legend Title

You can set title for legend using `title` property in `legendSettings`. You can also customize the `fontStyle`, `size`, `fontWeight`, `color`, `textAlignment`, `fontFamily`, `opacity` and `textOverflow` of legend title. `titlePosition` is used to set the legend position in `Top`, `Left` and `Right` position. `maximumTitleWidth` is used to set the width of the legend title. By default, it will be `100px`.

{% tab template="chart/axis/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
      { country: "China", gold: 40, silver: 60, bronze: 55 },
      { country: "Japan", gold: 70, silver: 60, bronze: 50 },
      { country: "Australia", gold: 60, silver: 56, bronze: 40 },
      { country: "France", gold: 50, silver: 45, bronze: 35 },
      { country: "Germany", gold: 40, silver: 30, bronze: 22 },
      { country: "Italy", gold: 40, silver: 35, bronze: 37 },
      { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public primaryxAxis: AxisModel = {
   valueType: 'Category'
  };
  public primaryyAxis: AxisModel = {
     minimum: 0, maximum: 80, interval: 20, title: 'Medals'
  };
  public legendSettings: LegendSettingsModel = {
    visible: true, title: 'Countries'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' type='Column'
          name='December 2007'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' type='Column'
          name='December 2008'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' type='Column'
          name='December 2009'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Arrow Page Navigation

By default, the page number will be enabled while legend paging. Now, you can disable that page number and also you can get left and right arrows for page navigation. You have to set `false` value to `enablePages` to get this support.

{% tab template="chart/axis/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, LineSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'WW', y: 12, y1: 22, y2: 38.3, y3: 50 },
    { x: 'EU', y: 9.9, y1: 26, y2: 45.2, y3: 63.6 },
    { x: 'APAC', y: 4.4, y1: 9.3, y2: 18.2, y3: 20.9 },
    { x: 'LATAM', y: 6.4, y1: 28, y2: 46.7, y3: 65.1 },
    { x: 'MEA', y: 30, y1: 45.7, y2: 61.5, y3: 73 },
    { x: 'NA', y: 25.3, y1: 35.9, y2: 64, y3: 81.4 }
  ];
  public primaryxAxis: AxisModel = {
    title: 'Countries', valueType: 'Category', interval: 1,
    labelIntersectAction: 'Rotate45'
  };
  public primaryyAxis: AxisModel = {
    title: 'Penetration (%)', rangePadding: 'None', labelFormat: '{value}%',
    minimum: 0, maximum: 90
  };
  public legendSettings: LegendSettingsModel = {
    width: '180', enablePages: false
  };
  public marker1 = { visible: true, width: 10, height: 10, shape: 'Diamond' };
  public marker2 = { visible: true, width: 10, height: 10, shape: 'Pentagon' };
  public marker3 = { visible: true, width: 10, height: 10, shape: 'Triangle' };
  public marker4 = { visible: true, width: 10, height: 10, shape: 'Circle' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' type='Line' width={2}
          name='December 2007' marker={this.marker1} >
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' type='Line' width={2}
          name='December 2008' marker={this.marker2} >
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y2' type='Line' width={2}
          name='December 2009' marker={this.marker3} >
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y3' type='Line' width={2}
          name='December 2010' marker={this.marker4} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note: To use legend feature, we need to inject `Legend` module into the `services`.

## See Also

* [Customize each shape in legend](./how-to/#customize-each-shape-in-legend)