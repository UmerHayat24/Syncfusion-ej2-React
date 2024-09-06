---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Customize the series points by using patterns

You can customize the series points by using the `pointColorMapping` property.

To customize the series point colors, follow the given steps:

**Step 1**:

Customize the point colors to set the color value by using the `pointColorMapping` property.

{% tab template="chart/pattern-point", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,AxisModel,CornerRadiusModel,
         Legend,  Category, Tooltip, DataLabel, ColumnSeries, IPointRenderEventArgs}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'BGD', y: 106, text: 'Bangaladesh', color: 'url(#chess)' },
    { x: 'BTN', y: 103, text: 'Bhutn', color: 'url(#cross)' },
    { x: 'NPL', y: 198, text: 'Nepal', color: 'url(#circle)' },
    { x: 'THA', y: 189, text: 'Thiland', color: 'url(#rectangle)' },
    { x: 'MYS', y: 250, text: 'Malaysia', color: 'url(#line)' }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 300, interval: 50 };
  public cornerradius: CornerRadiusModel = { bottomLeft: 10, bottomRight: 10, topLeft: 10, topRight: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryxAxis}
      title='Tiger Population - 2016'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' width={2} name='Tiger' pointColorMapping='color'
          type='Column' cornerRadius={this.cornerradius} >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}