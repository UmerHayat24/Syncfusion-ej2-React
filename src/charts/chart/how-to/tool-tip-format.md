---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Format the tooltip value

Using [`tooltipRender`](../../api/chart/chartModel/#tooltiprender) event, you can able to format the
datetime value instead of rendered value.

To format the datetime value,please follow the steps below

**Step 1**:

By using [`tooltipRender`](../../api/chart/chartModel/#tooltiprender) event we can able to get
the current point x value. Using this value to format the tooltip by using `formatDate` method.

The output will appear as follows,

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, LineSeries, ITextRenderEventArgs, ITooltipRenderEventArgs,AxisModel,TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { Internationalization } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: new Date(2005, 0, 1), y: 21 }, { x: new Date(2006, 0, 1), y: 24 },
    { x: new Date(2007, 0, 1), y: 30 }, { x: new Date(2008, 0, 1), y: 38 },
    { x: new Date(2009, 0, 1), y: 54 }, { x: new Date(2010, 0, 1), y: 57 },
  ];
  public primaryxAxis: AxisModel = { valueType: 'DateTime' };
  public marker = { visible: true, height: 10, width: 10, dataLabel: { visible: true } };
  public tooltip: TooltipSettingsModel = { enable: true };
  public tooltipRender = (args: ITooltipRenderEventArgs) => {
    let intl: Internationalization = new Internationalization();
    let formattedString: string = intl.formatDate(new Date(args.point.x), { skeleton: 'yMd' });
    args.text = formattedString;
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Inflation - Consumer Price'
      tooltipRender={this.tooltipRender}
      tooltip={this.tooltip}>
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
