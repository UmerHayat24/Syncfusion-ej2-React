---
title: "Pie and Doughnut | TypeScript "

component: "Accumulation Chart"

description: "Pie and doughnut charts are used to presents the relationship of different parts of data and also known biggest data easily"
---

# Pie & Doughnut

## Pie Chart

To render a pie series, use the series [`type`](../api/accumulation-chart/accumulationSeriesModel/#type) as `Pie` and
inject the `PieSeries` module into the `services`. If the `PieSeries` module is not
injected, this module will be loaded by default.

{% tab template="chart/series/pie", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, PieSeries, Inject}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  render() {
    return <AccumulationChartComponent id='charts'>
      <Inject services={[PieSeries]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' type='Pie'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Radius customization

By default, radius of the pie series will be 80% of the size (minimum of chart width and height).
You can customize this using [`radius`](../api/accumulation-chart/accumulationSeries/#radius) property of the series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  render() {
    return <AccumulationChartComponent id='charts'>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' radius='100%'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Pie Center

The center position of the pie can be changed by Center X and Center Y. By default, center value of the pie series x and y is 50%. You can customize this using [`center`](../api/accumulation-chart/accumulationChartModel/#center)property of the series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
  Inject, AccumulationLegend, PieSeries, AccumulationTooltip,
  AccumulationDataLabel }
from'@syncfusion/ej2-react-charts';
import { data1 } from 'datasource.ts';

class App extends React.Component<{}, {}> {
  public pie: AccumulationChartComponent;
  render() {
   return <AccumulationChartComponent id='pie-chart' ref={pie => this.pie = pie}
              title='Mobile Browser Statistics'
              load={this.load.bind(this)}
              legendSettings={{ visible: false }}
              enableSmartLabels={true}
              enableAnimation={false}
              center={{x: '60%', y: '60%'}}
              tooltip={{ enable: false, format: '${point.x} : <b>${point.y}%</b>' }}
            >
              <Inject services={[AccumulationLegend, PieSeries, AccumulationTooltip, AccumulationDataLabel]} />
              <AccumulationSeriesCollectionDirective>
                <AccumulationSeriesDirective dataSource={data1} name='Browser' xName='x' yName='y'
                  explode={true} explodeOffset='10%' explodeIndex={0}
                  dataLabel={{
                    visible: true,
                    position: 'Inside', name: 'text',
                    font: {
                      fontWeight: '600'
                    }
                  }}
                  radius='70%'
                >
                </AccumulationSeriesDirective>
              </AccumulationSeriesCollectionDirective>
            </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Various Radius Pie Chart

You can use radius mapping to render the slice with different [`radius`](../api/accumulation-chart/accumulationSeries/#radius) pie and also use [`border`](../api/accumulation-chart/accumulationChartModel/#border) , fill properties to customize the point. dataLabel is used to represent individual data and its value.

{% tab template="chart/series/pie", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {  AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, AccumulationLegend, PieSeries, AccumulationDataLabel, AccumulationTooltip,
Inject } from'@syncfusion/ej2-react-charts';
import { variouspiedata } from 'datasource.ts';

class App extends React.Component<{}, {}> {
  public pie: AccumulationChartComponent;
  render() {
    return <AccumulationChartComponent id='pie-chart' ref={pie => this.pie = pie}
            legendSettings={{
              visible: true
            }}
            enableSmartLabels={true}
            enableAnimation={true}
            tooltip={{ enable: true }}
          >
            <Inject services={[AccumulationLegend, PieSeries, AccumulationDataLabel, AccumulationTooltip]} />
            <AccumulationSeriesCollectionDirective>
              <AccumulationSeriesDirective dataSource={data1} xName='x' yName='y' innerRadius='20%'
                dataLabel={{
                  visible: true, position: 'Outside', name: 'x'
                }}
                radius='r'
              >
              </AccumulationSeriesDirective>
            </AccumulationSeriesCollectionDirective>
          </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Doughnut Chart

To achieve a doughnut in pie series, customize the [`innerRadius`](../api/accumulation-chart/accumulationSeries/#innerradius)
property of the series. By setting value greater than 0%, a doughnut will appear.
The `innerRadius` property takes value from 0% to 100% of the pie radius.

{% tab template="chart/series/doughnut", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  render() {
    return <AccumulationChartComponent id='charts'>
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' innerRadius='40%'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Start and End angles

You can customize the start and end angle of the pie series using the
[`startAngle`](../api/accumulation-chart/accumulationSeries/#startangle) and
[`endAngle`](../api/accumulation-chart/accumulationSeries/#endangle) properties. The default value of  `startAngle` is 0 degree,
 and `endAngle` is 360 degrees. By customizing this, you can achieve a semi pie series.

{% tab template="chart/series/startangle", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, Inject, AccumulationDataLabel}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  render() {
    return <AccumulationChartComponent id='charts'>
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' startAngle='270' endAngle='90'
          dataLabel={{ visible: true, name: 'text', position: 'Outside' }}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Color & Text Mapping

The fill color and the text in the data source can be mapped to the chart using `pointColorMapping` in series and
`name` in datalabel respectively.

{% tab template="chart/series/startangle", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
Inject, AccumulationDataLabel,AccumulationDataLabelSettingsModel}
from'@syncfusion/ej2-react-charts';
import { dataMapping } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public datalabel: AccumulationDataLabelSettingsModel = { visible: true, name: 'text', position: 'Outside' };

  render() {
    return <AccumulationChartComponent id='charts'>
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={dataMapping} xName='x' yName='y' pointColorMapping='fill'
          dataLabel={this.datalabel}></AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customization

Individual points can be customized using the `pointRender` event.

{% tab template="chart/series/startangle", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective,IAccPointRenderEventArgs, AccumulationSeriesDirective, Inject, AccumulationDataLabel}
from'@syncfusion/ej2-react-charts';
import { dataMapping } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public onPointRender: EmitType<IAccPointRenderEventArgs> = (args: IAccPointRenderEventArgs): void => {
    if ((args.point.x as string).indexOf('Apr') > -1) {
      args.fill = '#f4bc42';
    }
    else {
      args.fill = '#597cf9';
    }
  };

  render() {
    return <AccumulationChartComponent id='charts' pointRender={this.onPointRender}>
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={dataMapping} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Hide pie or doughnut border

By default, the border will appear in the pie/doughnut chart while mouse hover on the chart. You can disable the the border by
setting `enableBorderOnMouseMove` property is `false`.

{% tab template="chart/series/startangle", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective,IAccPointRenderEventArgs, AccumulationSeriesDirective, Inject, AccumulationDataLabel}
from'@syncfusion/ej2-react-charts';
import { dataMapping } from 'datasource.ts';

class App extends React.Component<{}, {}> {
  render() {
    return <AccumulationChartComponent id='charts'
    enableBorderOnMouseMove={false}>
      <Inject services={[AccumulationDataLabel]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={dataMapping} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Multi-level pie chart

You can achieve a multi-level drill down in pie and doughnut charts using [pointClick](../../api/accumulation-chart/accumulationChartModel/#pointclick) event. If user clicks any point in the chart, that corresponding data will be shown in the next level and so on based on point clicked.

You can also achieve drill-up (back to the initial state) by using [chartMouseClick](../../api/accumulation-chart/accumulationChartModel/#chartmouseclick) event. In below sample, you can drill-up by clicking back button in the center of the chart.

{% tab template="chart/grid-visual", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Chart, AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, indexFinder, getElement, Inject, AccumulationDataLabel, AccumulationTooltip, PieSeries, AccumulationAnnotation, } from '@syncfusion/ej2-react-charts';
import { ColumnDirective, ColumnsDirective, GridComponent, Page, PageSettingsModel, Selection, Grid } from '@syncfusion/ej2-react-grids';

export class Drilldown extends React.Component<{}, {}> {

    public data: Object[] = [
        {
            x: 'SUV',
            y: 25,
            z: [
                {
                    title: 'Automobile Sales in the SUV Segment',
                    x: 'Toyota',
                    y: 8,
                    z: [
                        { x: '2000', y: 20 },
                        { x: '2001', y: 30 },
                        { x: '2002', y: 40 },
                    ],
                },
                { x: 'Ford', y: 12 },
                { x: 'GM', y: 17 },
                { x: 'Renault', y: 6 },
            ],
        },
        {
            x: 'Car',
            y: 37,
            z: [
                { title: 'Automobile Sales in the Car Segment', x: 'Toyota', y: 7 },
                { x: 'Chrysler', y: 12 },
                { x: 'Nissan', y: 9 },
                { x: 'Ford', y: 15 },
            ],
        },
        {
            x: 'Pickup',
            y: 15,
            z: [
                { title: 'Automobile Sales in the Pickup Segment', x: 'Nissan', y: 9 },
                { x: 'Chrysler', y: 4 },
                { x: 'Ford', y: 7 },
                { x: 'Toyota', y: 20 },
            ],
        },
        {
            x: 'Minivan',
            y: 23,
            z: [
                { title: 'Automobile Sales in the Minivan Segment', x: 'Hummer', y: 11 },
                { x: 'Ford', y: 5 },
                { x: 'GM', y: 12 },
                { x: 'Chrysler', y: 3 },
            ],
        },
    ];
    public grid: Grid | null;
    public pointIndex: number = -1;

    public dataLabel: Object = {
        visible: true, position: 'Inside', connectorStyle: { type: 'Curve', length: '5%' }, font: { size: '14px', color: 'white' }
    };
    public pointIndex: number = -1;
    public startAngle: number = 0;
    //public explodeIndex: number = 2;
    public endAngle: number = 360;
    public title: string = 'Automobile Sales by Category';
    public pie: AccumulationChartComponent;
    public isparent: boolean = true;
    render() {
        return (
            <div className='control-pane'>
                <div className='control-section'>
                    <AccumulationChartComponent id='pie-chart' ref={pie => this.pie = pie}
                        title='Automobile Sales by Category' enableSmartLabels={false} legendSettings={{ visible: false }}
                        tooltip={{ enable: false, format: '${point.x} <br> ${point.y} %' }}
                        chartMouseClick={this.onChartMouseClick.bind(this)}
                        pointClick={this.onPointClick.bind(this)}
                        textRender={this.onTextRender.bind(this)}>
                        <Inject services={[AccumulationDataLabel, AccumulationTooltip, PieSeries, AccumulationAnnotation]} />
                        <AccumulationSeriesCollectionDirective>
                            <AccumulationSeriesDirective dataSource={this.data} xName='x' yName='y' dataLabel={this.dataLabel} radius='70%'
                                explode={false} >
                            </AccumulationSeriesDirective>
                        </AccumulationSeriesCollectionDirective>
                    </AccumulationChartComponent>
                    <GridComponent ref={g => this.grid = g} dataSource={data} height='350'>
                        <ColumnsDirective>
                            <ColumnDirective field='x' headerText='Vehicle' type='string'></ColumnDirective>
                            <ColumnDirective field='y' headerText='Sales' type='string'></ColumnDirective>
                        </ColumnsDirective>
                    </GridComponent>
                </div>
            </div>
        )
    }
    public onTextRender(args: IAccTextRenderEventArgs): void {
        args.text = args.point.x + ' ' + args.point.y + ' %';
    }
    public onPointClick(args: IMouseEventArgs): void {
        if (getElement(pie.element.id + '_Series_' + args.seriesIndex + '_Point_' + args.pointIndex)) {
            this.pie.series[0].dataSource = data[args.pointIndex].z;
            this.pie.title = data[args.pointIndex].z[0].title;
            pointIndex = args.pointIndex;

            this.pie.series[0].name = 'Level 2';
            this.pie.series[0].innerRadius = '30%';
            this.pie.annotations = [
                {
                    content:
                        '<div id="back" style="cursor:pointer;padding:3px;width:30px; height:30px;">' +
                        '<img src="https://ej2.syncfusion.com/javascript/demos/src/chart/images/back.png" id="back" />',
                    region: 'Series',
                    x: '50%',
                    y: '50%',
                },
            ];
            this.pie.pointClick = click;
        }
        this.grid.dataSource = pie.series[0].dataSource;
        this.grid.columns[0].headerText = data[args.pointIndex].x;
        this.grid.refresh();
        this.pie.refresh();
    }

    public onChartMouseClick(args: IMouseEventArgs): void {
        if (args.target.indexOf('back') > -1) {
            if (pie.series[0].name === 'Level 3') {
                pie.series[0].dataSource = data[pointIndex].z;
                pie.series[0].name = 'Level 2';
                pie.title = data[pointIndex].z[0].title;
                pie.series[0].innerRadius = '30%';
                grid.dataSource = pie.series[0].dataSource;
                grid.columns[0].headerText = data[pointIndex].x;
                grid.refresh();
                pie.refresh();
            } else if (pie.series[0].name === 'Level 2') {
                pie.series[0].dataSource = data;
                pie.series[0].name = 'Level 1';
                pie.series[0].innerRadius = '0%';
                pie.title = 'Automobile Sales by Category';
                pie.annotations = null;
                pie.pointClick = pointClick;
                grid.dataSource = pie.series[0].dataSource;
                grid.columns[0].headerText = 'Vehicle';
                grid.refresh();
                pie.refresh();
            }
        }
        grid.dataSource = pie.series[0].dataSource;
    },
    pointClick: onPointClick,
    tooltip: { enable: false, format: '${point.x} <br> ${point.y} %' },
    title: 'Automobile Sales by Category',

    public click(args: IMouseEventArgs): void {
    if(pie.series[0].name !== 'Level 3') {
    switch (args.pointIndex) {
        case 0:
            pie.series[0].dataSource = data[0].z[0].z;
            pie.title = 'SUV Sales by Years';
            pie.series[0].name = 'Level 3';
            grid.columns[0].headerText = 'Year';
            grid.refresh();
            pie.refresh();
            break;
    }
    grid.dataSource = pie.series[0].dataSource;
 }
 };
}

ReactDOM.render(<Drilldown />, document.getElementById("charts"));
```

{% endtab %}

## See Also

* [Data label](./data-label/)
* [Grouping](./grouping/)
