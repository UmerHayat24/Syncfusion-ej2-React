---
title: " Chart Internationalization | React "

component: "Chart"

description: "Chart provides the support for internationalization for dataLabel, axis label and tooltip elements."
---

# Internationalization

Chart provide supports for internationalization for below chart elements.

* Datalabel.
* Axis label.
* Tooltip.

For more information about number and date formatter you can refer
[`internationalization`](http://ej2.syncfusion.com/documentation/base/intl.html).

<!-- markdownlint-disable MD036 -->
**Globalization**

Globalization is the process of designing and developing an component that works in different
cultures/locales.  Internationalization  library is used to globalize number, date, time values in
Chart component using  `labelFormat` property in axis.

**Numeric Format**

In the below example axis, point  and tooltip labels are globalized to EUR.

{% tab template="chart/axis/double", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Tooltip, DataLabel, TooltipSettingsModel, AxisModel }
from'@syncfusion/ej2-react-charts';
import { loadCldr, setCurrencyCode } from '@syncfusion/ej2-base';
setCurrencyCode('EUR');

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 1900, y: 4, y1: 2.6, y2: 2.8 }, { x: 1920, y: 3.0, y1: 2.8, y2: 2.5 },
    { x: 1940, y: 3.8, y1: 2.6, y2: 2.8 }, { x: 1960, y: 3.4, y1: 3, y2: 3.2 },
    { x: 1980, y: 3.2, y1: 3.6, y2: 2.9 }, { x: 2000, y: 3.9, y1: 3, y2: 2 }
  ];
  public primaryxAxis: AxisModel = { edgeLabelPlacement: 'Shift', title: 'Years' };
  public primaryyAxis: AxisModel = { labelFormat: 'c', title: 'Sales Amount in Millions' };
  public marker = { dataLabel: { visible: true } };
  public tooltip: TooltipSettingsModel = { enable: true, format: '${point.x} : ${point.y}' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'
      tooltip={this.tooltip}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Product X' type='Column'
          marker={this.marker}>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Product Y' type='Column'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}