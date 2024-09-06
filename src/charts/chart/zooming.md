---
title: " Chart Zooming | React "

component: "Chart"

description: "Chart have zooming and panning properties. Chart contains different  zoom modes, zoom toolbar items, scrollbar and auto interval zooming. "
---

# Zooming  and Panning

To get start quickly with React Chart Zooming and Panning, you can check on this video:

`youtube:6Fq99_MnpSA`

## Enable Zooming

Chart can be zoomed in three ways.

* Selection - By setting
[`enableSelectionZooming`](../api/chart/zoomSettingsModel/#enableselectionzooming)
property to true in `zoomSettings`, you can zoom the chart by using the rubber band selection.
* Mousewheel - By setting
[`enableMouseWheelZooming`](../api/chart/zoomSettingsModel/#enablemousewheelzooming) property to true
  in `zoomSettings`, you can zoomin and zoomout the chart by scrolling the mouse wheel.
* Pinch - By setting  [`enablePinchZooming`](../api/chart/zoomSettingsModel/#enablepinchzooming)
property to true in `zoomSettings`, you can zoom the chart through pinch gesture in touch enabled devices.

 >Note: Pinch zooming is supported only in browsers that support multi-touch gestures. Currently IE11,
Chrome and Opera browsers support multi-touch in desktop devices.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,ZoomSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries,  Zoom}
from'@syncfusion/ej2-react-charts';
import { zoomData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public legendSettings: LegendSettingsModel = { visible: false };
  public zoomsettings: ZoomSettingsModel = {
    enableMouseWheelZooming: true, enablePinchZooming: true,
    enableSelectionZooming: true
  };
  public border = { width: 0.5, color: '#00bdae' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      zoomSettings={this.zoomsettings}
      title='Sales History of Product X'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Zoom, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={zoomData} xName='x' yName='y' opacity={0.3} name='Product X' type='Area'
          border={this.border} animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

After zooming the chart, a zooming toolbar will appear with `zoom`,`zoomin`, `zoomout`, `pan` and `reset` buttons.
Selecting the Pan option will allow to pan the chart and selecting the Reset option will reset the zoomed chart.

## Modes

The [`mode`](../api/chart/zoomSettingsModel/#mode) property in zoomSettings specifies whether the c
hart is allowed to scale along the horizontal axis or vertical axis. The default value of the mode is XY (both axis).

There are three types of mode.

* X - Allows us to zoom the chart horizontally.
* Y - Allows us to zoom the chart vertically.
* XY - Allows us to zoom the chart both vertically and horizontally.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,ZoomSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries,  Zoom}
from'@syncfusion/ej2-react-charts';
import { zoomData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public legendSettings: LegendSettingsModel = { visible: false };
  public zoomsettings: ZoomSettingsModel = { mode: 'X', enableSelectionZooming: true };
  public border = { width: 0.5, color: '#00bdae' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      zoomSettings={this.zoomsettings}
      title='Sales History of Product X'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Zoom, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={zoomData} xName='x' yName='y' opacity={0.3} name='Product X' type='Area'
          border={this.border} animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Toolbar

By default, zoomin, zoomout, pan and reset buttons will be displayed for zoomed chart.
You can customize to show your desire tools in the toolbar using
[`toolbarItems`](../api/chart/zoomSettingsModel/#toolbaritems) property.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,ZoomSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries,  Zoom}
from'@syncfusion/ej2-react-charts';
import { zoomData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public legendSettings: LegendSettingsModel = { visible: false };
  public zoomsettings: ZoomSettingsModel = { enableSelectionZooming: true, toolbarItems: ['Zoom', 'Pan', 'Reset'] };
  public border = { width: 0.5, color: '#00bdae' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      zoomSettings={this.zoomsettings}
      title='Sales History of Product X'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Zoom, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={zoomData} xName='x' yName='y' name='Product X' opacity={0.3} type='Area'
          border={this.border} animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Eanble Scrollbar

Using [`enableScrollbar`](../api/chart/zoomSettingsModel/#enablescrollbar) property, you can able to add scrollbar for zoomed chart.
Using this scrollbar, you can pan or zoom the chart.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,ZoomSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries,  Zoom, ScrollBar }
from'@syncfusion/ej2-react-charts';
import { zoomData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', zoomFactor: 0.2, zoomPosition: 0.6 };
  public legendSettings: LegendSettingsModel = { visible: false };
  public zoomsettings: ZoomSettingsModel = { enableSelectionZooming: true, enableScrollbar: true };
  public border = { width: 0.5, color: '#00bdae' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      zoomSettings={this.zoomsettings}
      title='Sales History of Product X'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Zoom, DateTime, ScrollBar]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={zoomData} xName='x' yName='y' name='Product X' opacity={0.3} type='Area'
          border={this.border} animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Enable Pan

Using [`enablePan`](../api/chart/zoomSettingsModel/#enablepan) property you can able to
pan the zoomed chart without help of toolbar items.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,ZoomSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries,  Zoom}
from'@syncfusion/ej2-react-charts';
import { zoomData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', zoomFactor: 0.2, zoomPosition: 0.6 };
  public legendSettings: LegendSettingsModel = { visible: false };
  public zoomSettings: ZoomSettingsModel = { enableSelectionZooming: true, enablePan: true };
  public border = { width: 0.5, color: '#00bdae' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      zoomSettings={this.zoomSettings}
      title='Sales History of Product X'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Zoom, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={zoomData} xName='x' yName='y' name='Product X' opacity={0.3} type='Area'
          border={this.border} animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Auto interval on zooming

By using [`enableAutoIntervalOnZooming`](../api/chart/axis/#enableautointervalonzooming) property,
the axis interval will get calculated automatically with respect to the zoomed range.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,ZoomSettingsModel,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries,  Zoom}
from'@syncfusion/ej2-react-charts';
import { zoomData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'DateTime', enableAutoIntervalOnZooming: true };
  public legendSettings: LegendSettingsModel = { visible: false };
  public zoomSettings: ZoomSettingsModel = { enableSelectionZooming: true };
  public border = { width: 0.5, color: '#00bdae' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      zoomSettings={this.zoomSettings}
      title='Sales History of Product X'>
      <Inject services={[AreaSeries, Legend, Tooltip, DataLabel, Zoom, DateTime]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={zoomData} xName='x' yName='y' name='Product X' opacity={0.3} type='Area'
          border={this.border} animation={this.animation}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

>Note: To use zooming feature, we need to inject `Zoom` module into the `services`.