---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Show percentage value in pie tooltip

By using the [`tooltipRender`](../../api/chart/chartModel/#tooltiprender) event,
you can show the percentage value for each point of pie series in tooltip.

To show the percentage value in pie tooltip, follow the given steps:

**Step 1**:

By using the [`tooltipRender`](../../api/chart/chartModel/#tooltiprender) event,
you can get the `args.point.y` and `args.series.sumOfPoints` values. You can use these values to calculate the percentage
value for each point of pie series. To display the percentage value in tooltip, use the `args.content` property.

The output will appear as follows,

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
  IAccTooltipRenderEventArgs, Inject, AccumulationDataLabel, AccumulationTooltip, PieSeries,
  AccumulationDataLabelSettingsModel,TooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import{ EmitType } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { 'x': 'Chrome', y: 37 }, { 'x': 'UC Browser', y: 17 },
    { 'x': 'iPhone', y: 19 }, { 'x': 'Others', y: 4, text: '4' },
    { 'x': 'Opera', y: 11 }
  ];
  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, position: 'Inside', name: 'text' };
  public tooltip: TooltipSettingsModel = { enable: true };
  public tooltipRender: EmitType<IAccTooltipRenderEventArgs> = (args: IAccTooltipRenderEventArgs): void => {
    let value: any = args.point.y / args.series.sumOfPoints * 100;
    args.text = args.point.x + '' + Math.ceil(value) + '' + '%';
  };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip} title='Mobile Browser Statistics'
      tooltipRender={this.tooltipRender}>
      <Inject services={[AccumulationTooltip, PieSeries, AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' radius='70%' dataLabel={this.datalabel}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}