---
title: " Chart Appearance | React "

component: "Chart"

description: "We can customize chart appearance by using color palette, point level customization, chart area cutomization, title and margin customizations."
---

# Appearance

## Custom Color Palette

You can customize the default color of series or points by providing a custom color palette of your choice by
using the [`palettes`](../api/chart/chartModel/#palettes) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50, silver: 70, bronze: 45 },
    { country: "China", gold: 40, silver: 60, bronze: 55 },
    { country: "Japan", gold: 70, silver: 60, bronze: 50 },
    { country: "Australia", gold: 60, silver: 56, bronze: 40 },
    { country: "France", gold: 50, silver: 45, bronze: 35 },
    { country: "Germany", gold: 40, silver: 30, bronze: 22 },
    { country: "Italy", gold: 40, silver: 35, bronze: 37 },
    { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
  ];
  public palette: string[] = ["#E94649", "#F6B53F", "#6FAAB0", "#C4C24A"];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      palettes={this.palette}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          legendShape='Circle' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='silver' type='Column'
          name='Silver' legendShape='Rectangle'>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='bronze' name='Bronze'
          legendShape='Rectangle' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Point Level Customization

Marker, datalabel and fill color of each data point can be customized with
[`pointRender`](../api/chart/chartModel/#pointrender) and
[`textRender`](../api/chart/chartModel/#textrender) event.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,IPointRenderEventArgs}
from'@syncfusion/ej2-react-charts';
import { EmitType} from '@syncfusion/ej2-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50 },
    { country: "China", gold: 40 },
    { country: "Japan", gold: 70 },
    { country: "Australia", gold: 60 },
    { country: "France", gold: 50 },
    { country: "Germany", gold: 40 },
    { country: "Italy", gold: 40 },
    { country: "Sweden", gold: 30 }
  ];
  public pointRender: EmitType<IPointRenderEventArgs> = (args: IPointRenderEventArgs): void => {
    let seriesColor: string[] = ['#00bdae', '#404041', '#357cd2', '#e56590', '#f8b883',
      '#70ad47', '#dd8abd', '#7f84e8', '#7bb4eb', '#ea7a57'];
    args.fill = seriesColor[args.point.index];
  };
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      pointRender={this.pointRender}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

## Chart Area Customization

<!-- markdownlint-disable MD036 -->

**Customize the Chart Background**

<!-- markdownlint-disable MD013 -->
Using [`background`](../api/chart/chartModel/#background) and [`border`](../api/chart/chartModel/#border) properties, you can change the background color and border of the chart.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject, BorderModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50 },
    { country: "China", gold: 40 },
    { country: "Japan", gold: 70 },
    { country: "Australia", gold: 60 },
    { country: "France", gold: 50 },
    { country: "Germany", gold: 40 },
    { country: "Italy", gold: 40 },
    { country: "Sweden", gold: 30 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public border: BorderModel = { width: 2, color: '#FF0000' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      background='skyblue' border={this.border}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Chart Margin**

You can set margin for chart from its container through [`margin`](../api/chart/chartModel/#margin) property.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,BorderModel,MarginModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50 },
    { country: "China", gold: 40 },
    { country: "Japan", gold: 70 },
    { country: "Australia", gold: 60 },
    { country: "France", gold: 50 },
    { country: "Germany", gold: 40 },
    { country: "Italy", gold: 40 },
    { country: "Sweden", gold: 30 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public border: BorderModel = { width: 2, color: '#FF0000' };
  public margin: MarginModel = { left: 40, right: 40, top: 40, bottom: 40 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      background='skyblue' border={this.border}
      margin={this.margin}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Chart Area Customization**

Using [`background`](../api/chart/chartAreaModel/#background) and [`border`](../api/chart/chartAreaModel/border/) properties, you can change the background color and border of the chart area. Width for the chart area can be customized using [`width`](../api/chart/chartAreaModel/width/) property.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,BorderModel,ChartAreaModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50 },
    { country: "China", gold: 40 },
    { country: "Japan", gold: 70 },
    { country: "Australia", gold: 60 },
    { country: "France", gold: 50 },
    { country: "Germany", gold: 40 },
    { country: "Italy", gold: 40 },
    { country: "Sweden", gold: 30 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public border: BorderModel = { width: 2, color: '#FF0000' };
  public chartarea: ChartAreaModel = { background: 'skyblue', width: '90%' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      border={this.border}
      chartArea={this.chartarea}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Animation

You can customize animation for a particular series using [`animation`](../api/chart/animationModel/) property. You can enable or disable animation of the series using `enable` property, `duration` specifies the duration of an animation and `delay` allows us to start the animation at desire time.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { country: "USA", gold: 50 },
    { country: "China", gold: 40 },
    { country: "Japan", gold: 70 },
    { country: "Australia", gold: 60 },
    { country: "France", gold: 50 },
    { country: "Germany", gold: 40 },
    { country: "Italy", gold: 40 },
    { country: "Sweden", gold: 30 }
  ];
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };
  public border = { width: 2, color: 'grey' };
  public animation = { enable: true, duration: 1200, delay: 100 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='country' yName='gold' name='Gold'
          border={this.border}
          animation={this.animations} type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Fluid Animation

Fluid animation used to animate series with updated dataSource continues animation rather than animation whole series. You can customize animation for a particular series using [`animate`] method.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 'Egg', y: 106 },
    { x: 'Fish', y: 103 },
    { x: 'Misc', y: 198 },
    { x: 'Tea', y: 189 },
    { x: 'Fruits', y: 250 }
  ];
  public primaryxAxis: AxisModel = {{ valueType: 'Category', interval: 1, tickPosition: 'Inside',
                        labelPosition:'Inside', labelStyle: { color: '#ffffff' } }};
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 300, interval: 50, labelStyle: { color: 'transparent' } };
  public onChartLoad(args: ILoadedEventArgs): void {
        let chart: Element = document.getElementById('charts2');
        chart.setAttribute('title', '');
        args.chart.loaded = null;
        let columninterval = setInterval(
            () => {
                if (document.getElementById('charts2')) {
                    if (count === 0) {
                        args.chart.series[0].dataSource = [
                            { x: 'Egg', y: 206 },
                            { x: 'Fish', y: 123},
                            { x: 'Misc', y: 48 },
                            { x: 'Tea', y: 240 },
                            { x: 'Fruits', y: 170 }
                        ];
                        args.chart.animate();
                        count++;
                    }
                    else if (count === 1) {
                        args.chart.series[0].dataSource = [
                            { x: 'Egg', y: 86 },
                            { x: 'Fish', y: 173 },
                            { x: 'Misc', y: 188 },
                            { x: 'Tea', y: 109 },
                            { x: 'Fruits', y: 100 }
                        ];
                        args.chart.animate();
                        count++;
                    }
                    else if (count === 2) {
                        args.chart.series[0].dataSource = [
                            { x: 'Egg', y: 156 },
                            { x: 'Fish', y: 33 },
                            { x: 'Misc', y: 260 },
                            { x: 'Tea', y: 200 },
                            { x: 'Fruits', y: 30 }
                        ];
                        args.chart.animate();
                        count = 0;
                    }
                } else {
                    clearInterval(columninterval);
                }
            },
            2000
        );
  },

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals'  loaded={this.onChartLoad.bind(this)}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
         <SeriesCollectionDirective>
                            <SeriesDirective dataSource={this.data} type='Column' xName='x' width={2} yName='y' name='Tiger'
                                cornerRadius={{ bottomLeft: 10, bottomRight: 10, topLeft: 10, topRight: 10 }}
                                marker={{ dataLabel: { visible: true, position: 'Top', font: { fontWeight: '600', color: '#ffffff' } } }}>
                            </SeriesDirective>
                        </SeriesCollectionDirective>
    </ChartComponent>
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Chart Title

Chart can be given a title using [`title`](../api/chart/chartModel/#title) property, to show the information about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,FontModel,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public data: any[] = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
    public primaryxAxis: AxisModel= {title: 'Years',lineStyle: { width: 0 },labelFormat: 'y',
           intervalType: 'Years',valueType: 'DateTime',edgeLabelPlacement: 'Shift'}  ;
    public primaryyAxis: AxisModel= {title: 'Percentage (%)',labelFormat: '{value}%',
           minimum: 0, maximum: 20, interval: 2}  ;
    public titlestyle:FontModel ={fontFamily: "Arial", fontStyle: 'italic',fontWeight: 'regular',
           color: "#E27F2D", size: '23px'};
    public marker={ visible: true, width: 10, height: 10 };

    render(){
            return <ChartComponent id='charts'
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    title='Unemployment Rates 1975-2010'
                    titleStyle = { this.titlestyle }>
                      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]}/>
                      <SeriesCollectionDirective>
                          <SeriesDirective dataSource ={this.data}  xName='x' yName='y' name='China' width={2}
                           type='StepLine' marker={ this.marker }>
                          </SeriesDirective>
                          <SeriesDirective dataSource ={this.data}  xName='x' yName='y1' name='Australia' width={2}
                           type='StepLine' marker={ this.marker }>
                          </SeriesDirective>
                          <SeriesDirective dataSource ={this.data}  xName='x' yName='y2' name='Japan' width={2}
                           type='StepLine' marker={this.marker }>
                          </SeriesDirective>
                      </SeriesCollectionDirective>
                  </ChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

**Title wrap**

The `textStyle` property of chart title provides options to customize the `size`, `color`, `fontFamily`, `fontWeight`,
`fontStyle`, `opacity`, `textAlignment` and `textOverflow`.

{% tab template="chart/series/column", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, LineSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public data: any[] = [
      { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
      { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
      { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
      { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
      { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
      { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
    ];
    public primaryxAxis: AxisModel= { valueType: 'Category', title: 'Countries'}  ;
    public textstyle={ size:'18px', color:'Red', textAlignment: 'Far', textOverflow: 'Wrap' };

    render(){
      return <ChartComponent id='charts'
                  primaryXAxis={ this.primaryxAxis }
                  textStyle= {this.textstyle }
                  title='Sales Analysis'>
                    <Inject services={[Legend, Tooltip, DataLabel, Category, LineSeries]}/>
                    <SeriesCollectionDirective>
                        <SeriesDirective dataSource ={this.data}  xName='month' yName='sales'
                         type='Line'>
                        </SeriesDirective>
                    </SeriesCollectionDirective>
                </ChartComponent>
    }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Chart SubTitle

Chart can be given a subtitle using [`subTitle`](../api/chart/chartModel/#subtitle) property, to show the information
about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,FontModel,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{},{}> {

    public data: any[] = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
    public primaryxAxis: AxisModel= {title: 'Years',lineStyle: { width: 0 },labelFormat: 'y',
           intervalType: 'Years',valueType: 'DateTime',edgeLabelPlacement: 'Shift'}  ;
    public primaryyAxis: AxisModel= {title: 'Percentage (%)',labelFormat: '{value}%',
           minimum: 0, maximum: 20, interval: 2}  ;
    public subtitlestyle:FontModel ={fontFamily: "Arial", fontStyle: 'italic',fontWeight: 'regular',
           color: "#E27F2D"};
    public marker={ visible: true, width: 10, height: 10 };

    render(){
            return <ChartComponent id='charts'
                    primaryXAxis={ this.primaryxAxis }
                    primaryYAxis={ this.primaryyAxis }
                    title='Unemployment Rates 1975-2010'
                    subTitle='(1975-2010)'
                    subTitleStyle = { this.subtitlestyle }>
                      <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]}/>
                      <SeriesCollectionDirective>
                          <SeriesDirective dataSource ={this.data}  xName='x' yName='y' name='China' width={2}
                           type='StepLine' marker={ this.marker }>
                          </SeriesDirective>
                          <SeriesDirective dataSource ={this.data}  xName='x' yName='y1' name='Australia' width={2}
                           type='StepLine' marker={ this.marker }>
                          </SeriesDirective>
                          <SeriesDirective dataSource ={this.data}  xName='x' yName='y2' name='Japan' width={2}
                           type='StepLine' marker={this.marker }>
                          </SeriesDirective>
                      </SeriesCollectionDirective>
                  </ChartComponent>
      }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## See Also

* [Customize the series points using patterns](./how-to/#customize-the-series-points-by-using-patterns)