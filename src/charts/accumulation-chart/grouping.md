---
title: "Accumulation Chart Grouping | React "

component: "Accumulation Chart"

description: "By using point and value in pie chart,you can group collection of points into the single slice."
---

# Grouping

You can club/group few points of the series based on
[`groupTo`](../api/accumulation-chart/accumulationSeriesModel/#groupto) property. For example, if the club
value is 11, then the points with value less than 11 is grouped together and will be showed as a single
point with label `others`. The property also takes value in percentage (percentage of total data points value).

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
   Inject, AccumulationDataLabel,AccumulationDataLabelSettingsModel,
  IAccTextRenderEventArgs, IAccPointRenderEventArgs
  }
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, name: 'text', position: 'Outside' };

  render() {
    return <AccumulationChartComponent id='charts' >
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' groupTo='11'
          dataLabel={this.datalabel}></AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Broken slice

You can visualize all points available in club/group points by clicking on the grouped point. For example,
if 5 points are grouped together it will be showed as a single slice with label `others`. If we click on `others`
slice it will explode and broke into 5 seperate slices.

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
   Inject, AccumulationDataLabel,AccumulationDataLabelSettingsModel,
  IAccTextRenderEventArgs, IAccPointRenderEventArgs
  }
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {
  public dataSource:any[] = [
                    { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                    { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                    { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                    { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                    { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' },
                    { x: 'Nov', y: 9, text: 'Nov: 9' }, { x: 'Dec', y: 3.5, text: 'Dec: 3.5' }
                ];
  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, name: 'text', position: 'Outside' };

  render() {
    return <AccumulationChartComponent id='charts' >
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={this.dataSource} xName='x' yName='y' groupTo='11' explode={true} explodeOffset='10'
          dataLabel={this.datalabel}></AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## GroupMode

Slice can also be grouped based on number of points by specifying the `groupMode` to Point. For example, if the
group to value is 11, accumulation chart will show 1st 11 points and will group remaining entries in the collection
as a single point.

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject, AccumulationDataLabel,
  IAccTextRenderEventArgs, IAccPointRenderEventArgs,AccumulationDataLabelSettingsModel
  }
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, name: 'text', position: 'Outside' };

  render() {
    return <AccumulationChartComponent id='charts'>
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' groupTo='4' groupMode='Point'
          dataLabel={this.datalabel}></AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customization

You can customize the grouped point and its data label using `pointRender` and `textRender` event.

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject, AccumulationDataLabel,
  IAccTextRenderEventArgs, IAccPointRenderEventArgs,AccumulationDataLabelSettingsModel
  }
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public onTextRender: EmitType<IAccTextRenderEventArgs> = (args: IAccTextRenderEventArgs): void => {
    if (args.text.indexOf('Others') > -1) {
      args.color = 'red';
      args.border.width = 1;
    }
  };
  public onPointRender: EmitType<IAccPointRenderEventArgs> = (args: IAccPointRenderEventArgs): void => {
    if ((args.point.x as string).indexOf('Others') > -1) {
      args.fill = '#D3D3D3';
    }
  };
  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, name: 'text', position: 'Outside' };

  render() {
    return <AccumulationChartComponent id='charts' textRender={this.onTextRender} pointRender={this.onPointRender}>
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' groupTo='11'
          dataLabel={this.datalabel}></AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}