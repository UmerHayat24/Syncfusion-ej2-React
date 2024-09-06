---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Customize the marker with different shape

By using the [`pointRender`](../../api/chart/chartModel/#pointrender), you can customize the marker shape.

To Customize the marker shape, follow the given steps:

**Step 1**:

Customize the marker shape in each data point by using the [`pointRender`](../../api/chart/chartModel/#pointrender) event.
Using this event, you can set the `shape` value to the argument.

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, AxisModel,
         Legend,  Category, Tooltip, DataLabel, LineSeries, Marker, IPointRenderEventArgs}
from'@syncfusion/ej2-react-charts';
import { EmitType} from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'WW', y: 12, text: 'World Wide' },
    { x: 'EU', y: 5, text: 'Europe' },
    { x: 'APAC', y: 15, text: 'Pacific' },
    { x: 'LATAM', y: 6.4, text: 'Latin' },
    { x: 'MEA', y: 30, text: 'Africa' },
    { x: 'NA', y: 25.3, text: 'America' }
  ];
  public pointRender: EmitType<IPointRenderEventArgs> = (args: IPointRenderEventArgs): void => {
    let shapes: string[] = ['Diamond', 'Circle', 'Rectangle', 'Line', 'Triangle', 'Rectangle'];
    args.shape = shapes[args.point.index];
  };
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 60, interval: 15 };
  public marker = {
    visible: true, width: 10, height: 10,
    shape: 'Diamond'
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='FB Penetration of Internet Audience'
      pointRender={this.pointRender}>
      <Inject services={[LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' width={2} name='December 2007'
          type='Line' marker={this.marker} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
  ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}