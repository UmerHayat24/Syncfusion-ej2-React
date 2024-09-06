---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Get the data of clicked area in accumulation chart

By using the [`pointClick`](https://ej2.syncfusion.com/react/documentation/api/chart/#pointclick) event, you can get the chart data of clicked area.

To show the clicked area data from pie, follow the given steps:

**Step 1**:

By using the [`pointClick`](https://ej2.syncfusion.com/react/documentation/api/chart/#pointclick) event, you can get the `args.point.x` and `args.point.y` values.

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
  IPointEventArgs, Inject, AccumulationDataLabel, AccumulationTooltip, PieSeries,
  AccumulationDataLabelSettingsModel,TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import{ EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public data: any[] = [
     { 'x': 'Chrome', y: 37, text: '37%' }, { 'x': 'UC Browser', y: 17, text: '17%' },
    { 'x': 'iPhone', y: 19, text: '19%' },{ 'x': 'Others', y: 4, text: '4%' },
     { 'x': 'Opera', y: 11, text: '11%' }, { 'x': 'Android', y: 12, text: '12%' }
  ];
  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, position: 'Inside', name: 'text' };
  public pointClick: EmitType<IPointEventArgs> = (args: IPointEventArgs): void => {
      document.getElementById("lbl").innerText = "X : "+ args.point.x + "\nY : "+ args.point.y;
  };

  render() {
    return(<div>
    <label id="lbl"></label>
     <AccumulationChartComponent id='charts'  title='Mobile Browser Statistics'
      pointClick={this.pointClick}>
      <Inject services={[AccumulationTooltip, PieSeries, AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' radius='70%' dataLabel={this.datalabel}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent></div>)
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}