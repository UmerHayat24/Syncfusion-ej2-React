---
title: " Chart Axis Customization | React "

component: "Chart"

description: "Chart axis contains different customization and types like axis crossing, multiple axis, inversed axis, tick and grid, title customizations"
---

# Axis Customization

## Axis Crossing

An axis can be positioned in the chart area using `crossesAt` and `crossesInAxis` properties.
The `crossesAt` property specifies the values (datetime, numeric, or logarithmic) at which the axis line has to be intersected with the vertical axis or vice-versa, and the `crossesInAxis` property specifies the axis name with which the axis line has to be crossed.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection
}
  from '@syncfusion/ej2-react-charts';
import { stripData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { crossesAt: 15 };
  public primaryyAxis: AxisModel = { crossesAt: 5 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
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

## Title

You can add a title to the axis using [`title`](../api/chart/axisModel/#title) property to provide quick
information to the user about the data plotted in the axis. Title style can be customized using `titleStyle`
property of the axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection
}
  from '@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category', title: 'Countries', titleStyle: {
      size: '16px', color: 'blue', fontFamily: 'Segoe UI', fontWeight: 'bold'
    }
  };

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

## Tick Lines Customization

You can customize the  `width`, `color` and `size` of the minor and major tick lines, using
[`majorTickLines`](../api/chart/axisModel/#majorticklines) and
[`minorTickLines`](../api/chart/axisModel/#minorticklines) properties in the axis.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection
}
  from '@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    majorTickLines: {
      color: 'blue',
      width: 5
    },
    minorTickLines: {
      color: 'red',
      width: 0
    }
  };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)',
    majorTickLines: {
      color: 'blue',
      width: 5
    },
    minorTickLines: {
      color: 'red',
      width: 0
    }
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Temperature flow over months'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' name='Sales' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Grid Lines Customization

You can customize the `width`, `color` and `dashArray` of the minor and major grid lines,
using [`majorGridLines`](../api/chart/axisModel/#majorgridlines) and
[`minorGridLines`](../api/chart/axisModel/#minorgridlines) properties in the axis.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection
}
  from '@syncfusion/ej2-react-charts';
import { categoryData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = {
    valueType: 'Category',
    majorGridLines: {
      color: 'blue',
      width: 1
    },
    minorGridLines: {
      color: 'red',
      width: 0
    }
  };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)',
    majorGridLines: {
      color: 'blue',
      width: 1
    },
    minorGridLines: {
      color: 'red',
      width: 0
    }
  };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Temperature flow over months'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={categoryData} xName='country' yName='gold' name='Sales' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Multiple Axis

In addition to primary X and Y axis, we can add n number of axis to the chart. Series can be associated with
this axis, by mapping with axis's unique name.

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, Tooltip, DataLabel, Zoom, Crosshair, LineSeries, Selection
}
  from '@syncfusion/ej2-react-charts';
import { PaneData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public primaryyAxis: AxisModel = {
    title: 'Temperature (Fahrenheit)', minimum: 0, maximum: 90, interval: 10,
    lineStyle: { width: 0 }, labelFormat: '{value}°F'
  };
  public marker = { visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' } };
  public lines = { width: 0 };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Temperature flow over months'>
      <Inject services={[ColumnSeries, LineSeries, Legend, Tooltip, DataLabel, Category]} />
      <AxesDirective>
        <AxisDirective rowIndex={0} name='yAxis1' opposedPosition={true} title='Temperature (Celsius)'
          majorGridLines={this.lines} lineStyle={this.lines} >
        </AxisDirective>
      </AxesDirective>
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={PaneData} xName='x' yName='y' name='Germany' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={PaneData} xName='x' yName='y1' name='Japan' type='Line'
          marker={this.marker} yAxisName='yAxis1' >
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Inversed Axis

When an axis is inversed, highest value of the axis comes closer to origin and vice versa. To place an axis in inversed manner set this property
 [`isInversed`](../api/chart/axisModel/#isinversed) to true.

 {% tab template="chart/axis/multiple", sourceFiles="app/**/*.tsx", compileJsx=true %}

 ```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, DataLabel
}
  from '@syncfusion/ej2-react-charts';
import { inverseData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', opposedPosition: true, isInversed: true };
  public primaryyAxis: AxisModel = { title: 'Exchange rate (INR per USD)', isInversed: true };
  public marker = { dataLabel: { visible: true } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Exchange Rate'>
      <Inject services={[ColumnSeries, Category, Legend, DataLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={inverseData} xName='x' yName='y' type='Column' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Opposed Position

To place an axis opposite from its original position, set
[`opposedPosition`](../api/chart/axisModel/#opposedposition) property of the axis to true.

{% tab template="chart/series/line", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  AxisModel, ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
  ColumnSeries, Legend, Category, DataLabel
}
  from '@syncfusion/ej2-react-charts';
import { inverseData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { title: 'Years', opposedPosition: true };
  public primaryyAxis: AxisModel = { title: 'Exchange rate (INR per USD)' };
  public marker = { dataLabel: { visible: true } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Exchange Rate'>
      <Inject services={[ColumnSeries, Category, Legend, DataLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={inverseData} xName='x' yName='y' type='Column' marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}