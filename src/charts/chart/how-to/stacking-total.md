---
title: " Chart How To | React "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Show the total value for stacking series in data label

By using the `annotation`, you can show any element in desired view.

To show the total value in data points, follow the given steps:

**Step 1**:

Define annotation for each x point in chart, now change the annotation value in chart by using
the [`annotationRender`](../../api/chart/chartModel/#annotationrender) event.
In this event, assign the stacked value of the last series to the annotation to show the total value of the
stacking series.

{% tab template="chart/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,AnnotationsDirective, AnnotationDirective,
         Legend,  Category, Tooltip, DataLabel, StackingColumnSeries, IAnnotationRenderEventArgs, ChartAnnotation ,AxisModel}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Jamesh', y0: 5, y1: 4, y2: 5 },
    { x: 'Michael', y0: 4, y1: 3, y2: 4 },
    { x: 'John', y0: 5, y1: 4, y2: 2 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 15, interval: 5 };
  public marker1 = { visible: true, dataLabel: { position: 'Top', font: { fontWeight: '600', color: '#ffffff' } } };
  public marker2 = { visible: true, dataLabel: { position: 'Top', font: { fontWeight: '600', color: '#ffffff' } } };
  public marker3 = { visible: true, dataLabel: { position: 'Top', font: { fontWeight: '600', color: '#ffffff' } } };
  public template1: any = this.chartTemplate1;
  public chartTemplate1(): any {
    return (<div className='template'>
      <div style={{ color: 'gray',fontSize:'11px',fontWeight:'bold',fill: 'gray'}}>
        <span>11</span>
      </div>
    </div>);
  };
  public template2: any = this.chartTemplate2;
  public chartTemplate2(): any {
    return (<div className='template'>
      <div style={{ color: 'gray',fontSize:'11px',fontWeight:'bold',fill: 'gray'}}>
        <span>10</span>
      </div>
    </div>);
  };
  public template3: any = this.chartTemplate3;
  public chartTemplate3(): any {
    return (<div className='template'>
      <div style={{ color: 'gray',fontSize:'11px',fontWeight:'bold',fill: 'gray'}}>
        <span>12</span>
      </div>
    </div>);
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryxAxis}
      title='Fruit Consumption' >
      <Inject services={[StackingColumnSeries, Legend, Tooltip, DataLabel, Category, ChartAnnotation]} />
      <AnnotationsDirective>
        <AnnotationDirective content={this.template1} coordinateUnits='Point' x='Jamesh' y={14.5}>
        </AnnotationDirective>
        <AnnotationDirective content={this.template2} coordinateUnits='Point' x='Michael' y={12}>
        </AnnotationDirective>
        <AnnotationDirective content={this.template3} coordinateUnits='Point' x='John' y={12}>
        </AnnotationDirective>
      </AnnotationsDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} type='StackingColumn' xName='x' yName='y0' name='Apple'
          marker={this.marker1} ></SeriesDirective>
        <SeriesDirective dataSource={this.data} type='StackingColumn' xName='x' yName='y1' name='Orange'
          marker={this.marker2}></SeriesDirective>
        <SeriesDirective dataSource={this.data} type='StackingColumn' xName='x' yName='y2' name='Grapes'
          marker={this.marker3} ></SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}