---
title: " Chart Crosshair and Trackball | React "

component: "Chart"

description: "Crosshair has a vertical and horizontal line to view the value of the axis at mouse position.The trackball used to display data collections"
---

# Crosshair

Crosshair has a vertical and horizontal line to view the value of the axis at mouse or touch position.

Crosshair lines can be enabled by using [`enable`](../api/chart/crosshairSettings/#enable) property in
the `crosshair`. Likewise tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltipModel/#enable)
property of `crosshairTooltip` in the corresponding axis.

{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,CrosshairSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, LineSeries,  Crosshair}
from'@syncfusion/ej2-react-charts';
import { data } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public crosshair: CrosshairSettingsModel = { enable: true };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      crosshair={this.crosshair}
      title='Sales History of Product X'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Crosshair, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='Product X' type='Line'
          marker={this.marker} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Tooltip for axis

Tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltipModel/#enable)
property of `crosshairTooltip` in the corresponding axis.

{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,CrosshairSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, LineSeries,  Crosshair}
from'@syncfusion/ej2-react-charts';
import { data } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', crosshairTooltip: { enable: true } };
  public primaryyAxis: AxisModel = { crosshairTooltip: { enable: true } };
  public crosshair: CrosshairSettingsModel = { enable: true };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      crosshair={this.crosshair}
      title='Sales History of Product X'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Crosshair, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='Product X' type='Line'
          marker={this.marker} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Customization

The [`fill`](../api/chart/crosshairTooltip/#fill) and [`textStyle`](../api/chart/crosshairTooltip/#textstyle)
property of the `crosshairTooltip` is used to customize the background color and font style of the crosshair label
respectively. Color and width of the crosshair line can be customized by using the [`line`](../api/chart/crosshairSettings/#line)
property in the crosshair.

{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,CrosshairSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, LineSeries,  Crosshair}
from'@syncfusion/ej2-react-charts';
import { data } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', crosshairTooltip: { enable: true, fill: 'green' } };
  public primaryyAxis: AxisModel = { crosshairTooltip: { enable: true, fill: 'green' } };
  public crosshair: CrosshairSettingsModel = { enable: true, line: { width: 2, color: 'green' } };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      crosshair={this.crosshair}
      title='Sales History of Product X'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Crosshair, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y' name='Product X' type='Line'
          marker={this.marker} >
        </SeriesDirective>
        <SeriesDirective dataSource={data} xName='x' yName='y1' name='Product X' type='Line'
          marker={this.marker} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

>Note: To use crosshair feature, we need to inject `Crosshair` module into the `services`.

## Trackball

Trackball is used to track a data point closest to the mouse or touch position. Trackball marker
indicates the closest point and trackball tooltip displays the information about the point.
To use trackball feature, we need to inject `Crosshair` and `Tooltip` module into the `services`.

Trackball can be enabled by setting the [`enable`](../api/chart/crosshairSettings/#enable) property
of the crosshair to true and [`shared`](../api/chart/tooltipSettings/#shared) property
in `tooltip` to true in chart.

{% tab template="chart/user-interaction/trackball", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,CrosshairSettingsModel,TooltipSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, LineSeries,  Crosshair}
from'@syncfusion/ej2-react-charts';
import { trackData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Years', minimum: new Date(2000, 1, 1),
    maximum: new Date(2006, 2, 11), intervalType: 'Years', valueType: 'DateTime'
  };
  public primaryyAxis: AxisModel = { crosshairTooltip: { enable: true, fill: 'green' } };
  public crosshair: CrosshairSettingsModel = { enable: true, lineType: 'Vertical' };
  public marker = { visible: true };
  public tooltip: TooltipSettingsModel = { enable: true, shared: true, format: '${series.name} : ${point.x} : ${point.y}' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      crosshair={this.crosshair}
      tooltip={this.tooltip}
      title='Average Sales per Person'>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Crosshair, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={trackData} xName='x' yName='y' name='John' type='Line' width={2}
          marker={this.marker} >
        </SeriesDirective>
        <SeriesDirective dataSource={trackData} xName='x' yName='y1' name='Andrew' type='Line' width={2}
          marker={this.marker} ></SeriesDirective>
        <SeriesDirective dataSource={trackData} xName='x' yName='y2' name='Thomas' type='Line' width={2}
          marker={this.marker} ></SeriesDirective>
        <SeriesDirective dataSource={trackData} xName='x' yName='y3' name='Mark' type='Line' width={2}
          marker={this.marker} ></SeriesDirective>
        <SeriesDirective dataSource={trackData} xName='x' yName='y4' name='William' type='Line' width={2}
          marker={this.marker} ></SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}