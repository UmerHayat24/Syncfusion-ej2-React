---
title: " Chart Strip-lines | React "

component: "Chart"

description: "Strip Lines are vertical or horizontal lines used to highlight/mark a certain region on the plot area."
---

<!-- markdownlint-disable MD036 -->

# Strip lines

<!-- markdownlint-disable MD036 -->

EJ2 chart supports horizontal and vertical strip lines and customization of stripline in both orientation.
To use strip line feature, you need to inject `StripLine` into the `services`.

## Horizontal Strip lines

You can create Horizontal stripline by adding the `stripline` in the vertical axis and set `visible` option to true.
Striplines are rendered in the specified start to end range and you can add more than one stripline for an axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Overs' };
  public primaryyAxis: AxisModel = {
    title: 'Runs',
    stripLines: [{ start: 15, end: 22, text: 'Good', color: '#ff512f', visible: true },
    { start: 8, end: 15, text: 'Medium', color: 'pink', opacity: 0.5, visible: true },
    { start: 0, end: 8, text: 'Not enough', color: 'skyblue', opacity: 0.5, visible: true }]
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='India Vs Australia 1st match'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stripData} xName='x' yName='y' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Vertical Striplines

You can create vertical stripline by adding the`stripline` in the horizontal axis and set `visible` option to true.
Striplines are rendered in the specified start to end range and you can add more than one stripline for an axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Overs', stripLines: [{ start: 0, end: 5, text: 'powerplay 1', color: 'red', visible: true, opacity: 0.5 },
    { start: 5, end: 10, text: 'powerplay 2', color: 'blue', visible: true, opacity: 0.5 }]
  };
  public primaryyAxis: AxisModel = { title: 'Runs' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='India Vs Australia 1st match'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stripData} xName='x' yName='y' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customize the strip line

Starting value in specific strip line can be customized by `start` property in strip line. Similarly, ending
value is customized by `end`. It can be also set for starting from the corresponding origin of the axis by
`startFromOrigin`. Size of the strip line is customized by `size`. Border for the stripline is customized
by `border`. Order of the strip line such that whether it should be rendered in behind or over the series elements
is customized by `zIndex`.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx


import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Overs', stripLines: [{ startFromOrigin: true, size: 4, zIndex: 'Behind', opacity: 0.5 }] };
  public primaryyAxis: AxisModel = { title: 'Runs' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='India Vs Australia 1st match'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stripData} xName='x' yName='y' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Customize the stripline text

You can customize the text rendered in stripline by `textStyle` property. Rotation of the strip line text can be
changed by `rotation` property. Horizontal and Vertical alignment of stripline text can be changed
by `horizontalAlignment` and `verticalAlignment` property.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx


import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    title: 'Overs', stripLines: [
      {
        startFromOrigin: true, size: 4, zIndex: 'Behind', opacity: 0.5, verticalAlignment: 'Middle', horizontalAlignment: 'End', rotation: 90,
        textStyle: { size: 15 }
      }, { start: 5, end: 8, verticalAlignment: 'Start', horizontalAlignment: 'End', rotation: 45 }]
  };
  public primaryyAxis: AxisModel = { title: 'Runs' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='India Vs Australia 1st match'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stripData} xName='x' yName='y' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Dash Array

You can create dash array stripline by using `dashArray` property. The Striplines are rendered with specified dash array values.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryyAxis: AxisModel = {  minimum: 0, maximum: 60, interval: 10,
        stripLines:[{ start: 30, size: 2, sizeType: 'Pixel', dashArray:"10,5", color: "red"}]
  };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={stripData} xName='x' yName='y' type='Column' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Recurrence Stripline

 The strip lines to be drawn repeatedly at the regular intervals – this will be useful when you want to mark an event that occurs recursively along the timeline of the chart. Following properties are used to configure this feature.

* `isRepeat`       - It is used for enable / disable the recurrence strip line.
* `repeatEvery`    - It is used for mention the stripline interval.
* `repeatUntil`    - It specifies the end value at which point strip line has to stop repeating.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [{x: 1, y: 5},{x: 2, y: 39},{x: 3, y: 21},{x: 4, y: 51},{x: 5, y: 30},
                             {x: 6, y: 25},{x: 7, y: 10},{x: 8, y: 40},{x: 9, y: 50},{x: 10, y: 20}];
  public primaryxAxis: AxisModel = { stripLines:[{start: 1, size: 1, isRepeat: true, repeatEvery: 2, color: 'rgba(167,169,171, 0.3)'}]
  };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='y' type='Line' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Size Type

The `sizeType` property refers the size of the stripline. They are,

* `Auto`
* `Pixel`
* `Years`
* `Months`
* `Days`
* `Hours`
* `Minutes`
* `Seconds`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,DateTime,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [{ x: new Date(2000, 0, 1), y: 10 }, { x: new Date(2002, 0, 1), y: 40 },
    { x: new Date(2004, 0, 1), y: 20 }, { x: new Date(2006, 0, 1), y: 50 },
    { x: new Date(2008, 0, 1), y: 15 }, { x: new Date(2010, 0, 1), y: 30 }];
  public primaryxAxis: AxisModel = { valueType: 'DateTime', intervalType: 'Years',
       stripLines:[{start:new Date(2002, 0, 1) , size: 2, sizeType: 'Years', color: 'rgba(167,169,171, 0.3)'}] };
  public primaryyAxis: AxisModel={ minimum: 0, maximum: 60, interval: 10 }
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries, Legend, LineSeries, Tooltip, DataLabel, DateTime, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='y' type='Line' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Segment Stripline

You can create stripline in a particular region with respect to segment. You can enable the segment stripline using `isSegmented` property. The start and end value of this type of stripline can be defined using `segmentStart` and `segmentEnd` properties.

* `isSegmented`     - It is used for enable the segment stripline.
* `segmentStart`    - Used to change the segment start value. Value correspond to associated axis.
* `segmentEnd`      - Used to change the segment end value. Value correspond to associated axis.
* `segmentAxisName` - Used to specify the name of the associated axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, StripLine,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries,  Selection, StripLinesDirective, StripLineDirective}
from'@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public chartData: any[] = [{x: 1, y: 5},{x: 2, y: 39},{x: 3, y: 21},{x: 4, y: 51},{x: 5, y: 30},
                             {x: 6, y: 25},{x: 7, y: 10},{x: 8, y: 40},{x: 9, y: 50},{x: 10, y: 20}];
  public primaryyAxis: AxisModel = { stripLines:[
            {start: 20, end: 40, isSegmented: true, segmentStart: 2, segmentEnd: 4,
            color: 'rgba(167,169,171, 0.3)'}
        ]
  };
  public marker = { visible: true };

  render() {
    return <ChartComponent id='charts'
       primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries,LineSeries, Legend, Tooltip, DataLabel, Category, StripLine]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.chartData} xName='x' yName='y' type='Line' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## See Also

* [Mark the threshold in chart](./how-to/#mark-a-threshold-in-chart)