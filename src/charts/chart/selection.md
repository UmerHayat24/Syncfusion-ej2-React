---
title: " Chart Selection | React "

component: "Chart"

description: "Strip Lines are vertical or horizontal lines used to highlight/mark a certain region on the plot area."
---
<!-- markdownlint-disable MD036 -->

# Selection

Chart provides selection support for the series and its data points on mouse click.

>When Mouse is clicked on the data points, the corresponding series legend will also be selected.

We have different type of selection mode for selecting the data. They are,

* None
* Point
* Series
* Cluster
* DragXY
* DragX
* DragY

## Point

 You can select a point, by setting `selectionMode` to point.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {  AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Olympic Medals' selectionMode='Point'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'>        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Series

 You can select a series, by setting `selectionMode` to series.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Olympic Medals' selectionMode='Series'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Cluster

You can select the points that corresponds to the same index in all the series, by setting `selectionMode` to cluster.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Olympic Medals' selectionMode='Cluster'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Rectangular selection

**DragXY, DragX and DragY**

To fetch the collection of data under a particular region, you have to set `selectionMode` as `DragXY`.

* DragXY - Allows us to select data with respect to horizontal and vertical axis.
* DragX - Allows us to select data with respect to horizontal axis.
* DragY - Allows us to select data with respect to vertical axis.

The selected data’s are returned as an array collection in the [`dragComplete`](../api/chart/chartModel/#dragcomplete)
event.

{% tab template="chart/user-interaction/drag", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip,Selection, DataLabel, ScatterSeries}
from'@syncfusion/ej2-react-charts';
import { dragData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { width: 12, height: 12 };

  render() {
    return <ChartComponent id='charts'
      selectionMode='DragXY'
      title='Height Vs Weight'>
      <Inject services={[ScatterSeries, Legend, Tooltip, Selection]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dragData} xName='x' yName='y' type='Scatter'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Lasso selection

To select a region by drawing freehand shapes to fetch a collection of data use `selectionMode` as `Lasso`. You can also select multiple regions on the chart through this mode.

{% tab template="chart/user-interaction/drag", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip,Selection, DataLabel, ScatterSeries}
from'@syncfusion/ej2-react-charts';
import { dragData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { width: 12, height: 12 };

  render() {
    return <ChartComponent id='charts'
      selectionMode='Lasso'
      title='Height Vs Weight'>
      <Inject services={[ScatterSeries, Legend, Tooltip, Selection]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dragData} xName='x' yName='y' type='Scatter'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Multi-region selection

To select multiple region on the chart, set the `allowMultiSelection` property to true.

{% tab template="chart/user-interaction/drag", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip,Selection, DataLabel, ScatterSeries}
from'@syncfusion/ej2-react-charts';
import { dragData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public marker = { width: 12, height: 12 };

  render() {
    return <ChartComponent id='charts'
      selectionMode='Lasso' allowMultiSelection={true}
      title='Height Vs Weight'>
      <Inject services={[ScatterSeries, Legend, Tooltip, Selection]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={dragData} xName='x' yName='y' type='Scatter'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Selection Type

You can select multiple points or series, by enabling the [`isMultiSelect`](../api/chart/chartModel/#ismultiselect) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import {  AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Olympic Medals' isMultiSelect={true} selectionMode='Point'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Selection on Load

You can able to select a point or series programmatically on a chart using
[`selectedDataIndexes`](../api/chart/chartModel/#selecteddataindexes) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public selectedData: any[] = [{ series: 0, point: 1 }, { series: 2, point: 3 }];
  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public animation = { enable: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      title='Olympic Medals' selectedDataIndexes={this.selectedData}
      isMultiSelect={true} selectionMode='Point'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'
          selectionStyle='chartSelection1' animation={this.animation} >  </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'
          selectionStyle='chartSelection2' animation={this.animation}> </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'
          selectionStyle='chartSelection3' animation={this.animation}> </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Selection through on legend

You can able to select a point or series through on legend using
[`toggleVisibility`](../api/chart/legendSettingsModel/#togglevisibility) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,LegendSettingsModel,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from  'datasource.ts';

class App extends React.Component<{}, {}> {

  public primaryxAxis: AxisModel = { valueType: 'Category' };
  public legendSettings: LegendSettingsModel = { visible: true, toggleVisibility: false };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      legendSettings={this.legendSettings}
      title='Olympic Medals' selectionMode='Point'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'>        </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Customization for selection

You can apply custom style to selected points or series with [`selectionStyle`](../api/chart/series/#selectionstyle) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AxisModel, ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries,  Selection}
from'@syncfusion/ej2-react-charts';
import { selectionData } from 'datasource.ts';

class App extends React.Component<{}, {}> {
  public primaryxAxis: AxisModel = { valueType: 'Category', title: 'Countries' };
  public primaryyAxis: AxisModel = { minimum: 0, maximum: 80, interval: 20, title: 'Medals' };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Olympic Medals' isMultiSelect={true} selectionMode='Point'>
      <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='gold' name='Gold' type='Column'
          selectionStyle='chartSelection1'>  </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='silver' name='Silver' type='Column'
          selectionStyle='chartSelection2'> </SeriesDirective>
        <SeriesDirective dataSource={selectionData} xName='country' yName='bronze' name='Bronze' type='Column'
          selectionStyle='chartSelection3'> </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

>Note: To use select feature, we need to Inject `Selection` module into the `services`.

## See Also

* [Display selected data for range selection](./how-to/#display-selected-data-for-range-selection)