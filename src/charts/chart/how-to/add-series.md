---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Add or remove a series from the chart dynamically

You can add or remove the chart series dynamically by using the `addSeries` or `removeSeries` method.

To add or remove the series dynamically, follow the given steps:

**Step 1**:

To add a new series to chart dynamically, pass the series value to the `addSeries` method.

To remove the new series from chart dynamically, pass the series index to the `removeSeries` method.

{% tab template="chart/add-series", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}>{

  public data: any[] = [{ x: 'John', y: 10000 },
  { x: 'Jake', y: 12000 },
  { x: 'Peter', y: 18000 },
  { x: 'James', y: 11000 },
  ];
  public chartInstance: ChartComponent;
  public add() {
    this.chartInstance.addSeries([{
      type: 'Column',
      dataSource: [{ x: 'John', y: 11000 }, { x: 'Jake', y: 16000 }, { x: 'Peter', y: 19000 },
      { x: 'James', y: 12000 }, { x: 'Mary', y: 10700 }],
      xName: 'x', width: 2,
      yName: 'y'
    }]);
  };
  public remove() {
    this.chartInstance.removeSeries(1);
  };

  render() {
    return (<div>
      <ButtonComponent value='add' cssClass='e-flat' onClick={this.add.bind(this)}>add</ButtonComponent>
      <ButtonComponent value='remove' cssClass='e-flat' onClick={this.remove.bind(this)}>remove</ButtonComponent>
      <ChartComponent id='charts' ref={chart => this.chartInstance = chart} primaryXAxis={{ valueType: 'Category' }}
        title='Sales Comparision'>
        <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, LineSeries, Category]} />
        <SeriesCollectionDirective>
          <SeriesDirective dataSource={this.data} xName='x' yName='y' type='Column' name='Sales'>
          </SeriesDirective>
        </SeriesCollectionDirective>
      </ChartComponent> </div>)
  }

};
ReactDOM.render(<App />, document.getElementById('charts'));
```

{% endtab %}