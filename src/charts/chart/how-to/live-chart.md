---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Create a live chart

You can update a chart with live data by using the set interval.

To update live data in a chart, follow the given steps:

**Step 1**:

Initialize the chart with series.

**Step 2**:

Update the data to series, and refresh the chart at specified interval by using the set interval.

To refresh the chart, invoke the `refresh` method.

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, LineSeries, ILoadedEventArgs}
from'@syncfusion/ej2-react-charts';
import { getElement } from '@syncfusion/ej2-charts';

class App extends React.Component<{}, {}>{
  constructor(props: any, chart: ChartComponent) {
    super(props)
    for (; this.i < 50; this.i++) {
      if (Math.random() > .5) {
          this.value += Math.random() * 2.0;
      }
      this.series1[this.i] = { x: this.i, y: this.value };
    }
    this.chart = chart;
  };

  public chart: ChartComponent;
  public series1: Object[] = [];
  public value: number = 10;  
  public intervalId: any;
  public setTimeoutValue: number = 100;
  public i: number = 0;
  public loaded(args: ILoadedEventArgs): void {
    this.intervalId = setTimeout(
      () => {
        if (this.chart === null) {
          clearInterval(this.intervalId);
        } else {
          if (Math.random() > .5) {
              this.value += Math.random() * 2.0;
          }
          this.i++;
          this.series1.push({ x: this.i, y: this.value });
          this.series1.shift();
          args.chart.series[0].dataSource = this.series1;
        }
      },
      this.setTimeoutValue);
  }

  render() {
    return <ChartComponent id='charts'
      loaded={this.loaded.bind(this) as EmitType<ILoadedEventArgs>}>
      <Inject services={[LineSeries]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.series1} xName='x' yName='y' type='Line'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('charts'));
```

{% endtab %}