---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# To make the scrollbar visible in initial rendering of chart

By setting `zoomFactor` in primaryXAxis and `isZoomed` value as `true` in
[`load`](../api/chart/chartModel/#load) event and `enableScrollbar` value as `true` in`zoomSettings`, you can make the scrollbar visible in initial rendering of chart.

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, Zoom,
         Legend, DateTime, Tooltip, DataLabel, LineSeries,  ILoadedEventArgs,AxisModel, ZoomSettingsModel, ScrollBar}
from'@syncfusion/ej2-react-charts';
import {  EmitType } from '@syncfusion/ej2-base'

 class App extends React.Component<{}, {}> {
  private chart1: ChartComponent;
  public data: any[] = [
    { x: new Date(2005, 0, 1), y: 21 },
    { x: new Date(2006, 0, 1), y: 24 },
    { x: new Date(2007, 0, 1), y: 36 },
    { x: new Date(2008, 0, 1), y: 38 },
    { x: new Date(2009, 0, 1), y: 54 },
    { x: new Date(2010, 0, 1), y: 21 },
    { x: new Date(2011, 0, 1), y: 24 },
    { x: new Date(2012, 0, 1), y: 36 },
    { x: new Date(2013, 0, 1), y: 38 },
    { x: new Date(2014, 0, 1), y: 54 },
    { x: new Date(2015, 0, 1), y: 21 },
    { x: new Date(2016, 0, 1), y: 24 },
    { x: new Date(2017, 0, 1), y: 36 },
    { x: new Date(2018, 0, 1), y: 38 },
  ];
  public zoomsettings: ZoomSettingsModel = {
    enableMouseWheelZooming: true,
    enablePinchZooming: true,
    enableSelectionZooming: true,
    mode: 'X',
    enableScrollbar: true,
  };
  public primaryxAxis: AxisModel = {  zoomFactor: 0.3,
            valueType: 'DateTime',
            labelFormat: 'y',
            intervalType: 'Years',
            edgeLabelPlacement:'Shift'};
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 100, interval: 10 };
  public marker = { visible: true, dataLabel: { visible: true } };
  public load: EmitType<ILoadedEventArgs> = (args: ILoadedEventArgs): void => {
      args.chart.zoomModule.isZoomed = true;
  };

  render() {
    return <ChartComponent id='charts'
      ref={chart => this.chart1 = chart}
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      zoomSettings={this.zoomsettings}
      title='Inflation - Consumer Price'
      load={this.load} >
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, DateTime, ScrollBar,Zoom]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' width={2} name='Germany'
          type='Line' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}