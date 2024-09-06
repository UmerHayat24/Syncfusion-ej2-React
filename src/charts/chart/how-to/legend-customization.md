---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Customize each shape in legend

By using the [`legendRender`](../../api/chart/chartModel/#legendrender), you can customize the legend shape.

To Customize the legend shape, follow the given steps:

**Step 1**:

Set the shape value for each legend using `args.shape` in
[`legendRender`](../../api/chart/chartModel/#legendrender) event.

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, AxisModel,
         Legend,  Category, Tooltip, DataLabel, StepAreaSeries , ILegendRenderEventArgs }
from'@syncfusion/ej2-react-charts';
import { EmitType} from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 2000, y: 416 }, { x: 2001, y: 490 },
    { x: 2002, y: 470 }, { x: 2003, y: 500 },
    { x: 2004, y: 449 }, { x: 2005, y: 470 },
    { x: 2006, y: 437 }, { x: 2007, y: 458 }
  ];
  public data1: any[] = [
    { x: 2000, y: 180 }, { x: 2001, y: 240 },
    { x: 2002, y: 370 }, { x: 2003, y: 200 },
    { x: 2004, y: 229 }, { x: 2005, y: 210 },
    { x: 2006, y: 337 }, { x: 2007, y: 258 }
  ];
  public legendRender: EmitType<ILegendRenderEventArgs> = (args: ILegendRenderEventArgs): void => {
    if (args.text === 'Renewable') {
      args.shape = 'Circle';
    } else if (args.text === 'Non-Renewable') {
      args.shape = 'Triangle';
    }
  };
  public primaryxAxis: AxisModel = { valueType: 'Double' };
  public primaryyAxis: AxisModel = { valueType: 'Double' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='FB Penetration of Internet Audience'
      legendRender={this.legendRender}>
      <Inject services={[StepAreaSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} type='StepArea' xName='x' yName='y' width={2} name='Renewable'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data1} type='StepArea' xName='x' yName='y' width={2} name='Non-Renewable' >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}
