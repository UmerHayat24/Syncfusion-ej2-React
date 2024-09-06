---
title: " Chart Axis Labels | React "

component: "Chart"

description: "Chart contains smart axis labels, label positioning, multilevelabels, text customization and sorting properties "
---

# Axis Labels

To get start quickly with Axis Labels in React Charts, you can check on this video:

`youtube:NLrOSKAnxes`

## Smart Axis Labels

When the axis labels overlap with each other, you can use
[`labelIntersectAction`](../api/chart/axisModel/#labelintersectaction) property in the axis, to place
them smartly.

When setting `labelIntersectAction` as `Hide`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection
} from '@syncfusion/ej2-react-charts';
import { smartAxisData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Countries', labelIntersectAction: 'Hide', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'People(in millions)', minimum: 0, maximum: 80, interval: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Internet Users'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={smartAxisData} xName='x' yName='y' name='Internet' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

When setting `labelIntersectAction` as `Rotate45`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { smartAxisData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Countries', labelIntersectAction: 'Rotate45', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'People(in millions)', minimum: 0, maximum: 80, interval: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Internet Users'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={smartAxisData} xName='x' yName='y' name='Internet' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

When setting `labelIntersectAction` as `Rotate90`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { smartAxisData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Countries', labelIntersectAction: 'Rotate90', valueType: 'Category' };
  public primaryyAxis: AxisModel = { title: 'People(in millions)', minimum: 0, maximum: 80, interval: 10 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Internet Users'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={smartAxisData} xName='x' yName='y' name='Internet' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Axis Labels Positioning

By default, the axis labels can be placed at `outside` the axis line and this also can be placed at `inside`
the axis line using the `labelPosition` property.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', labelPosition: 'Inside' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Multilevel Labels

Any number of levels of labels can be added to an axis using the `multiLevelLabels` property.
This property can be configured using the following properties:

• Categories
• Overflow
• Alignment
• Text style
• Border

>Note: To use multilevel label feature, we need to inject `MultiLevelLabel` module into the `services`.

### Categories

Using the categories property, you can configure the `start`, `end`, `text`, and `maximumTextWidth` of multilevel
labels.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection, MultiLevelLabel}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    multiLevelLabels: [{
      categories: [
        {//Start and end values of the multi-level labels accepts number, date and sring values
          start: -0.5,
          end: 3.5,
          //Multi-level label's text.
          text: 'Half Yearly 1'
        },
        { start: 3.5, end: 7.5, text: 'Half Yearly 2' },
      ]
    }]
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, MultiLevelLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Overflow

Using the `overflow` property, you can `trim` or `wrap` the multilevel labels.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection, MultiLevelLabel}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    multiLevelLabels: [{
      categories: [{ start: -0.5, end: 3.5, text: 'Half Yearly 1', maximumTextWidth: 50 },
      { start: 3.5, end: 7.5, text: 'Half Yearly 2', maximumTextWidth: 50 }],
      overflow: 'Trim'
    }]
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, MultiLevelLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

### Alignment

The `alignment` property provides option to position the multilevel labels at `far`, `center`, or `near`.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection, MultiLevelLabel}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    multiLevelLabels: [{
      categories: [{ start: -0.5, end: 3.5, text: 'Half Yearly 1' },
      { start: 3.5, end: 7.5, text: 'Half Yearly 2' }],
      alignment: 'Far'
    }]
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, MultiLevelLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

### Text customization

The `textStyle` property of multilevel labels provides options to customize the `size`, `color`, `fontFamily`,
`fontWeight`, `fontStyle`, `opacity`, `textAlignment` and `textOverflow`.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection, MultiLevelLabel}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    multiLevelLabels: [{
      categories: [{ start: -0.5, end: 3.5, text: 'Half Yearly 1' },
      { start: 3.5, end: 7.5, text: 'Half Yearly 2' }],
      textStyle: { size: '18px', color: 'Red' }
    }]
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, MultiLevelLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

### Border customization

Using the `border` property, you can customize the `width`, `color`, and `type`. The `type` of border are
`Rectangle`, `Brace`, `WithoutBorder`, `WithoutTopBorder`, `WithoutTopandBottomBorder` and `CurlyBrace`.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection, MultiLevelLabel}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    multiLevelLabels: [{
      categories: [{ start: -0.5, end: 3.5, text: 'Half Yearly 1' },
      { start: 3.5, end: 7.5, text: 'Half Yearly 2' }],
      border: { type: 'Brace', color: 'Blue', width: 2 },
    }]
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, MultiLevelLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Sorting

The chart’s data source can be sorted using the `sort` method of chart. The arguments that are required to pass to
sort method are data of chart. The fields depend on which sorting is performed either `x` or `y`, and the
`isDescending` with which data source values are sorted in either `ascending` or `descending`.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection }
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Edge Label Placement

Labels with long text at the edges of an axis may appear partially in the chart. To avoid this,
use [`edgeLabelPlacement`](../api/chart/axisModel/#edgelabelplacement) property in axis, which moves the
label inside the chart area for better appearance or hides it.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', edgeLabelPlacement: 'Shift' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Labels Customization

Border of the axis labels can be customized using `width`, `color` and `type` property of the axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category', border: { width: 1, type: 'Rectangle', color: 'red' } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Customizing Specific Point

You can customize the specific text in the axis labels using `axisLabelRender` event.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, IAxisLabelRenderEventArgs,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public axisLabelRender = (args: IAxisLabelRenderEventArgs) => {
    if (args.text === 'France') {
      args.labelStyle.color = 'Red';
    }
  }
  public primaryxAxis: AxisModel = { valueType: 'Category', border: { width: 1, type: 'Rectangle', color: 'red' } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      axisLabelRender={this.axisLabelRender}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Trim using maximum label width

You can trim the label using [`enableTrim`](../api/chart/axisModel/#enabletrim) property and width of the labels can also be customized using [`maximumLabelWidth`](../api/chart/axisModel/#maximumlabelwidth) property in the axis, the value maximum label width is `34` by default.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, IAxisLabelRenderEventArgs,
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { smartAxisData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

   public primaryxAxis: AxisModel = { valueType: 'Category',
        //label is trimmed
        enableTrim: true,
        //maximum width of label is provided
        maximumLabelWidth: '34',
   };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={smartAxisData} xName='x' yName='y' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Line break support

Line break feature used to customize the long axis label text into multiple lines by using
tag. Refer the below example in that dataSource x value contains long text, it breaks into two lines by using  `<br>` tag.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject, IAxisLabelRenderEventArgs,StackingColumnSeries
ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection}
from'@syncfusion/ej2-react-charts';
import { smartAxisData } from 'datasource.ts';

class App extends React.Component<{}, {}> {
public data1: any[] = [
    { x: 'Egg', y: 106 },
    { x: 'Fish', y: 103 },
    { x: 'Misc', y: 198 },
    { x: 'Tea', y: 189 },
    { x: 'Fruits', y: 250 }
];
   public primaryxAxis: AxisModel = { valueType: 'Category', interval: 1,tickPosition: 'Inside', labelPosition:'Inside', labelStyle: { color: '#ffffff' } };
  public primaryyAxis: AxisModel ={ minimum: 0, maximum: 300, interval: 50,  labelStyle: { color: 'transparent' } };
let count: number = 0;
  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}  primaryYAxis={this.primaryyAxis} title='Trade in Food Groups'
>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category,StackingColumnSeries]} />
         <SeriesCollectionDirective>
                            <SeriesDirective dataSource={data1} type='Column' xName='x' width={2} yName='y' name='Tiger'
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