---
title: " Accumulation Chart Annotation | React "

component: "Accumulation Chart"

description: "The annotations are used to mark the specific area of interest in the chart area with texts, shapes or images"
---

# Annotation

The annotations are used to mark the specific area of interest in the chart area with texts, shapes or images.

<!-- markdownlint-disable MD033 -->

By using the <code>content</code> option of annotation property, you can specify the Id of the element that needs
to be displayed in the chart area.

{% tab template="chart/series/accumulation", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject,AccumulationAnnotation, AccumulationAnnotationsDirective, AccumulationAnnotationDirective}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public template: any = this.chartTemplate;
  public chartTemplate(): any {
    return (<div className='template'>
      <div style={{ border: '1px solid black', backgroundColor: '#f5f5f5', padding: '5px 5px 5px 5px' }}>13.5</div>
    </div>);
  };

  render() {
    return <AccumulationChartComponent id='charts' >
      <Inject services={[AccumulationAnnotation]} />
      <AccumulationAnnotationsDirective>
        <AccumulationAnnotationDirective content={this.template} region='Series' coordinateUnits='Point' x='Feb' y={13.5}>
        </AccumulationAnnotationDirective>
      </AccumulationAnnotationsDirective>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

*Note: To use annotation feature in accumulation chart, we need to inject `AccumulationAnnotation` module into the `services`

## Region

The annotation can be placed with respect to either `Series` or `Chart`.

{% tab template="chart/series/accumulation", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject,AccumulationAnnotation, AccumulationAnnotationsDirective, AccumulationAnnotationDirective}
from'@syncfusion/ej2-react-charts';
import { labelData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public template:any=this.chartTemplate;
    public chartTemplate(): any {
         return (<div className='template'>
                    <div style={{ border: '1px solid black' ,backgroundColor:'#f5f5f5', padding: '5px 5px 5px 5px'}}>13.5</div>
                </div>);
    };

    render(){
        return <AccumulationChartComponent id='charts' >
            <Inject services={ [AccumulationAnnotation] } />
            <AccumulationAnnotationsDirective >
                <AccumulationAnnotationDirective content={ this.template } region = 'Chart' coordinateUnits= 'Pixel' x= { 550} y= { 150}>
                </AccumulationAnnotationDirective>
            </AccumulationAnnotationsDirective>
            <AccumulationSeriesCollectionDirective >
                <AccumulationSeriesDirective dataSource ={ labelData } xName = 'x' yName= 'y' >
                </AccumulationSeriesDirective>
            </AccumulationSeriesCollectionDirective>
        </AccumulationChartComponent>
      }

   };
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Co-ordinate Units

Specifies the coordinate units of an annotation either in `Pixel` or `Point`.

{% tab template="chart/series/accumulation", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject,AccumulationAnnotation, AccumulationAnnotationsDirective, AccumulationAnnotationDirective}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public template:any=this.chartTemplate;
    public chartTemplate(): any {
         return (<div className='template'>
                    <div style={{ border: '1px solid black' ,backgroundColor:'#f5f5f5', padding: '5px 5px 5px 5px'}}>13.5</div>
                </div>);
    };

    render(){
        return <AccumulationChartComponent id='charts' >
            <Inject services={[AccumulationAnnotation]}/>
            <AccumulationAnnotationsDirective>
                <AccumulationAnnotationDirective content={ this.template} region='Series' coordinateUnits='Point' x='Feb' y={13.5}>
                </AccumulationAnnotationDirective>
            </AccumulationAnnotationsDirective>
            <AccumulationSeriesCollectionDirective>
                <AccumulationSeriesDirective dataSource ={accData}  xName='x' yName='y'>
                </AccumulationSeriesDirective>
            </AccumulationSeriesCollectionDirective>
        </AccumulationChartComponent>
     }

  };
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Alignment

The annotations can be moved vertically and horizontally from its default position by using `verticalAlignment`
or `horizontalAlignment` properties. The verticalAlignment property takes value as `Top`, `Bottom` or `Middle` and the
horizontalAlignment property takes value as `Near`, `Far` or `Center`.

{% tab template="chart/series/accumulation", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject,AccumulationAnnotation, AccumulationAnnotationsDirective, AccumulationAnnotationDirective}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{},{}> {

    public template:any=this.chartTemplate;
    public chartTemplate(): any {
         return (<div className='template'>
                    <div style={{ border: '1px solid black' ,backgroundColor:'#f5f5f5', padding: '5px 5px 5px 5px'}}>13.5</div>
                </div>);
    };

    render(){
        return <AccumulationChartComponent id='charts' >
           <Inject services={[AccumulationAnnotation]}/>
           <AccumulationAnnotationsDirective>
                <AccumulationAnnotationDirective content={ this.template} region='Series' coordinateUnits='Point' x='Feb' y={13.5} verticalAlignment='Top' horizontalAlignment='Near'>
                </AccumulationAnnotationDirective>
           </AccumulationAnnotationsDirective>
           <AccumulationSeriesCollectionDirective>
                <AccumulationSeriesDirective dataSource ={accData}  xName='x' yName='y'>
                </AccumulationSeriesDirective>
            </AccumulationSeriesCollectionDirective>
        </AccumulationChartComponent>
    }

  };
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}
