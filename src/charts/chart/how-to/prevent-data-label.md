---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Prevent the data label when the data value is 0

To prevent the chart data label when the data value is 0, follow the given steps:

**Step 1**:

Get the point value and check whether the `args.point.y` value is zero or not by using the
[`textRender`](../../api/chart/chartModel/#textrender) event. If the value is zero,
then set the `args.cancel` to true.

The output will appear as follows,

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, LineSeries,  ITextRenderEventArgs,AxisModel}
from'@syncfusion/ej2-react-charts';
import {  EmitType } from '@syncfusion/ej2-base'

 class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: new Date(2005, 0, 1), y: 21 }, { x: new Date(2006, 0, 1), y: 24 },
    { x: new Date(2007, 0, 1), y: 0 }, { x: new Date(2008, 0, 1), y: 38 },
    { x: new Date(2009, 0, 1), y: 54 }, { x: new Date(2010, 0, 1), y: 57 },
  ];
  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 100, interval: 10 };
  public marker = { visible: true, dataLabel: { visible: true } };
  public textRender: EmitType<ITextRenderEventArgs> = (args: ITextRenderEventArgs): void => {
    if (args.text === '0') {
      args.cancel = args.point.y === 0;
    }
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Inflation - Consumer Price'
      textRender={this.textRender}>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, DateTime]} />
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