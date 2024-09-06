---
title: " Accumulation Chart Print and Export | React "

component: "Accumulation Chart"

description: "Accumultion chart have a public methods for print or export the rendered chart"
---

# Print and export

## Print

The rendered chart can be printed directly from the browser by calling the public method print.

{% tab template= "chart/print", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}>{

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public chartInstance: AccumulationChartComponent;
  public clickHandler() {
    this.chartInstance.print();
  }

  render() {
    return (<div>
      <button value='print' onClick={this.clickHandler.bind(this)}>Print</button>
      <AccumulationChartComponent id='charts' ref={chart => this.chartInstance = chart}>
        <AccumulationSeriesCollectionDirective>
          <AccumulationSeriesDirective dataSource={this.data} xName='month' yName='sales' radius='100%'>
          </AccumulationSeriesDirective>
        </AccumulationSeriesCollectionDirective>
      </AccumulationChartComponent></div>)
  }

};
ReactDOM.render(<App />, document.getElementById('charts'));

```

{% endtab %}

## Export

The rendered chart can be exported to `Image`(jpeg or png) or `SVG` or `PDF` format by using the export method.
Input parameters for this method are `Export` Type for `format` and `fileName` of result.

{% tab template= "chart/print", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}>{

  public data: any[] = [
    { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
    { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
    { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
    { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
    { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
    { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
  ];
  public chartInstance: AccumulationChartComponent;
  public clickHandler() {
    this.chartInstance.export('PNG', 'sample');
  }

  render() {
    return (<div><button value='print' onClick={this.clickHandler.bind(this)}>Export</button>
      <AccumulationChartComponent id='charts' ref={chart => this.chartInstance = chart}>
        <AccumulationSeriesCollectionDirective>
          <AccumulationSeriesDirective dataSource={this.data} xName='month' yName='sales' radius='100%'>
          </AccumulationSeriesDirective>
        </AccumulationSeriesCollectionDirective>
      </AccumulationChartComponent></div>)
  }

};
ReactDOM.render(<App />, document.getElementById('charts'));
```

{% endtab %}
