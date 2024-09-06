---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Create footer and watermark for chart

By using `annotation`, you can place any html elements to chart in a desired view.

To create footer and watermark for chart, follow the given steps:

**Step 1**:

Initialize the custom elements by using the `annotation` property.

By using the `content` option of the annotation object, you can specify the id of the element that needs to
be displayed in the chart area as follow,

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, ChartAnnotation, AnnotationsDirective, AnnotationDirective,
         Legend, Category, Tooltip, DataLabel, SplineSeries ,AxisModel}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Sun', y: 15 }, { x: 'Mon', y: 5 },
    { x: 'Tue', y: 32 }, { x: 'Wed', y: 15 },
    { x: 'Thu', y: 29 }, { x: 'Fri', y: 24 },
    { x: 'Sat', y: 18 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 60, interval: 20 };
  public marker = { visible: true };
  public animation = { enable: true, duration: 1200, delay: 100 };
  public content: any = this.chartTemplate;
  public chartTemplate(): any {
    return (<div className='template'>
      <a href="https://www.syncfusion.com" target="_blank">www.syncfusion.com</a>
    </div>);
  }

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals'>
      <Inject services={[SplineSeries, Legend, Tooltip, DataLabel, Category, ChartAnnotation]} />
      <AnnotationsDirective>
        <AnnotationDirective content={this.content} coordinateUnits='Point' x='Wed' y={20}>
        </AnnotationDirective>
        <AnnotationDirective content={this.content} coordinateUnits='Pixel' x={440} y={600}>
        </AnnotationDirective>
      </AnnotationsDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Max Temp' marker={this.marker}
          animation={this.animation} type='Spline'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}