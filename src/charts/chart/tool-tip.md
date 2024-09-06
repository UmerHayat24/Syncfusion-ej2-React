---
title: " Chart Tooltip | React "

component: "Chart"

description: "Tooltip is used to show the data value when mouse hover on the chart.We can able to customize format,template and appearance."
---

# Tooltip

Chart will display details about the points through tooltip, when the mouse is moved over the point

<!-- markdownlint-disable MD036 -->

## Default Tooltip

<!-- markdownlint-disable MD012 -->
By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/chart/tooltipSettingsModel/#enable) property to true and by injecting `Tooltip` module
into the `services`.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public tooltip: TooltipSettingsModel = { enable: true };
  public marker = { visible: true, width: 10, height: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      title='Unemployment Rates 1975-2010'>
      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='China' width={2}
          type='StepLine' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Format the Tooltip

By default, tooltip shows information of x and y value in points. In addition to that, you can show more
information in tooltip. For example the format '${series.name} ${point.x}' shows series name and point x
value.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public tooltip: TooltipSettingsModel = {
    enable: true, header: 'Unemployment',
    format: '<b>${point.x} : ${point.y}</b>'
  };
  public marker = { visible: true, width: 10, height: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      title='Unemployment Rates 1975-2010'>
      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='China' width={2}
          type='StepLine' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

## Individual Series Format

 You can format the each series tooltip separately using series `tooltipFormat` property.

 >Note: If series `tooltipFormat` is given, it shows the tooltip for that series in that format, or else it will take tooltip format.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, SplineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public tooltip: TooltipSettingsModel = {
    enable: true, header: 'Unemployment',
    format: '<b>${point.x} : ${point.y}</b>'
  };
  public marker = { visible: true, width: 10, height: 10 };
  public data1: object[] = [
                { x: 'Sun', y: 15 }, { x: 'Mon', y: 22 },
                { x: 'Tue', y: 32 },
                { x: 'Wed', y: 31 },
                { x: 'Thu', y: 29 }, { x: 'Fri', y: 24 },
                { x: 'Sat', y: 18 },
            ];
  public data2: object[] = [
                { x: 'Sun', y: 10 }, { x: 'Mon', y: 18 },
                { x: 'Tue', y: 28 },
                { x: 'Wed', y: 28 },
                { x: 'Thu', y: 26 }, { x: 'Fri', y: 20 },
                { x: 'Sat', y: 15 }
            ];
  public data3: object[] = [
                { x: 'Sun', y: 2 }, { x: 'Mon', y: 12 },
                { x: 'Tue', y: 22 },
                { x: 'Wed', y: 23 },
                { x: 'Thu', y: 19 }, { x: 'Fri', y: 13 },
                { x: 'Sat', y: 8 },
            ];
  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      title='Unemployment Rates 1975-2010'>
      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data1} xName='x' yName='y' name='Max Temp' width={2}
          type='Spline' marker={this.marker} tooltipFormat='${point.x}'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data2} xName='x' yName='y' name='Avg Temp' width={2}
          type='Spline' marker={this.marker} tooltipFormat='${point.y}'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data3} xName='x' yName='y' name='Min Temp' width={2}
          type='Spline' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

## Tooltip Template

Any HTML elements can be displayed in the tooltip by using the ‘template’ property of the tooltip. You can use the ${x} and ${y} as place holders in the HTML element to display the x and y values of the corresponding data point.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public template:any =this.chartTemplate;
  public tooltip: TooltipSettingsModel = {
    enable: true,
    template: this.template
  };
  public chartTemplate(args:any){
   return (<div id="templateWrap">
      <table style={{width:'100%',margin: '5px', border: '1px solid black' ,backgroundColor:'#00FFFF'}}>
        <tbody><tr><th colSpan={2}>Unemployment</th></tr>
          <tr><td>{args.x}</td><td>:</td><td>{args.y}</td></tr>
        </tbody>
      </table>
    </div>);
  }
  public marker = { visible: true, width: 10, height: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      title='Unemployment Rates 1975-2010'>
      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='China' width={2}
          type='StepLine' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Tooltip Mapping Name

By default, tooltip shows information of x and y value in points. You can show more information from data source in tooltip by using the `tooltipMappingName` property of the tooltip. You can use the `${point.tooltip}` as place holders to display the specified tooltip content.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,LegendSettingsModel,Category,
         Legend, DateTime, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';
import {chartData} from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public tooltip: TooltipSettingsModel = {enable: true, format: '${point.tooltip}'};
  public legendSettings: LegendSettingsModel = { visible: false};

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      legendSettings={this.legendSettings}
      title='Internet Users in Million – 2016'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, DateTime, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={chartData} xName='x' yName='y'
          type='Column' tooltipMappingName='country'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customize the Appearance of Tooltip

The [`fill`](../api/chart/tooltipSettingsModel/#fill) and [`border`](../api/chart/tooltipSettingsModel/#border) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](../api/chart/tooltipSettingsModel/#textstyle) property in the tooltip is used to customize the font of the tooltip text. The [`highlightColor`](../api/chart/#highlightcolor) property is used to customize the point color while hovering for tooltip.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,TooltipSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';
import { data } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public tooltip: TooltipSettingsModel = {
    enable: true, format: '${series.name} ${point.x} : ${point.y}',
    fill: '#7bb4eb', border: {
      width: 2,
      color: 'grey'
    }
  };
  public marker = { visible: true, width: 10, height: 10 };
  public titlestyle = {
    fontFamily: "Arial", fontStyle: 'italic', fontWeight: 'regular',
    color: "#E27F2D", size: '23px'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      tooltip={this.tooltip}
      title='Unemployment Rates 1975-2010'
      highlightColor='red'
      titleStyle={this.titlestyle}>
      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='China' width={2}
          type='StepLine' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## See Also

* [Format the tooltip value](./how-to/#format-the-tooltip-value)
* [Create a table in tooltip](./how-to/#create-a-table-in-tooltip)