---
title: " Chart User Interaction | React "

component: "Chart"

description: "It describes user interactions like tooltip, crosshair, trackball and data editing"
---

<!-- markdownlint-disable MD036 -->

# User Interaction

## Tooltip

Chart will display details about the points through tooltip, when the mouse is moved over the point

To get start quickly with React Chart Tooltip, you can check on this video:

`youtube:nQhhLNUzyM4`

**Enable Tooltip for Data Point**

<!-- markdownlint-disable MD012 -->
By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/chart/tooltipSettingsModel/#enable) property to true and by injecting `Tooltip` module
into the `services`.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',lineStyle: { width: 0 },labelFormat: 'y',
           intervalType: 'Years',valueType: 'DateTime',edgeLabelPlacement: 'Shift'} }
           primaryYAxis={ {title: 'Percentage (%)',labelFormat: '{value}%',
           minimum: 0, maximum: 20, interval: 2} }
           tooltip={ { enable: true} }
           title='Unemployment Rates 1975-2010'
           titleStyle = { {fontFamily: "Arial", fontStyle: 'italic',fontWeight: 'regular',
           color: "#E27F2D", size: '23px'} }>
    <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='China' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Australia' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y2' name='Japan' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);
```

{% endtab %}

**Format the Tooltip**

By default, tooltip shows information of x and y value in points. In addition to that, you can show more
information in tooltip. For example the format '${series.name} ${point.x}' shows series name and point x
value.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',lineStyle: { width: 0 },labelFormat: 'y',
           intervalType: 'Years',valueType: 'DateTime',edgeLabelPlacement: 'Shift'} }
           primaryYAxis={ {title: 'Percentage (%)',labelFormat: '{value}%',
           minimum: 0, maximum: 20, interval: 2} }
           tooltip={ { enable: true, format: '${series.name} ${point.x} : ${point.y}'} }
           title='Unemployment Rates 1975-2010'
           titleStyle = { {fontFamily: "Arial", fontStyle: 'italic',fontWeight: 'regular',
           color: "#E27F2D", size: '23px'} }>
    <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='China' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Australia' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y2' name='Japan' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

**Tooltip Template**

Any HTML elements can be displayed in the tooltip by using the ‘template’ property of the tooltip. You can use the ${x} and ${y} as place holders in the HTML element to display the x and y values of the corresponding data point.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',lineStyle: { width: 0 },labelFormat: 'y',
           intervalType: 'Years',valueType: 'DateTime',edgeLabelPlacement: 'Shift'} }
           primaryYAxis={ {title: 'Percentage (%)',labelFormat: '{value}%',
           minimum: 0, maximum: 20, interval: 2} }
           tooltip={ { enable: true,
           template: '<div style="background-color:lightblue"><div>${x}</div><div>${y}</div></div>'} }
           title='Unemployment Rates 1975-2010'
           titleStyle = { {fontFamily: "Arial", fontStyle: 'italic',fontWeight: 'regular',
           color: "#E27F2D", size: '23px'} }>
    <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='China' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Australia' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y2' name='Japan' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);
```

{% endtab %}

**Customize the Appearance of Tooltip**

The [`fill`](../api/chart/tooltipSettingsModel/#fill) and [`border`](../api/chart/tooltipSettingsModel/#border) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](../api/chart/tooltipSettingsModel/#textstyle) property in the tooltip is used to customize the font of the tooltip text.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, StepLineSeries}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',lineStyle: { width: 0 },labelFormat: 'y',
           intervalType: 'Years',valueType: 'DateTime',edgeLabelPlacement: 'Shift'} }
           primaryYAxis={ {title: 'Percentage (%)',labelFormat: '{value}%',
           minimum: 0, maximum: 20, interval: 2} }
           tooltip={ { enable: true, format: '${series.name} ${point.x} : ${point.y}',
           fill: '#7bb4eb',border: {
                   width: 2,
                   color: 'grey'
                } } }
           title='Unemployment Rates 1975-2010'
           titleStyle = { {fontFamily: "Arial", fontStyle: 'italic',fontWeight: 'regular',
           color: "#E27F2D", size: '23px'} }>
    <Inject services={[StepLineSeries, Legend, Tooltip, DataLabel, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='China' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Australia' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y2' name='Japan' width={2}
         type='StepLine' marker={ { visible: true, width: 10, height: 10 } }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);
```

{% endtab %}

## Zooming  and Panning

To get start quickly with React Chart Zooming and Panning, you can check on this video:

`youtube:6Fq99_MnpSA`

**Enable Zooming**

Chart can be zoomed in three ways.

* Selection - By setting
[`enableSelectionZooming`](../api/chart/zoomSettingsModel/#enableselectionzooming)
property to true in `zoomSettings`, you can zoom the chart by using the rubber band selection.
* Mousewheel - By setting
[`enableMouseWheelZooming`](../api/chart/zoomSettingsModel/#enablemousewheelzooming) property to true
  in `zoomSettings`, you can zoomin and zoomout the chart by scrolling the mouse wheel.
* Pinch - By setting  [`enablePinchZooming`](../api/chart/zoomSettingsModel/#enablepinchzooming)
property to true in `zoomSettings`, you can zoom the chart through pinch gesture in touch enabled devices.

 >Note: Pinch zooming is supported only in browsers that support multi-touch gestures. Currently IE11, Chrome and Opera browsers support multi-touch in desktop devices.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries, Zoom}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
              { x: new Date(2016, 0, 1), y: 7.1 }, { x: new Date(2016, 1, 1), y: 3.7 },
              { x: new Date(2016, 2, 1), y: 0.8 }, { x: new Date(2016, 3, 1), y: 6.3 },
              { x: new Date(2016, 4, 1), y: 13.3 }, { x: new Date(2016, 5, 1), y: 18.0 },
              { x: new Date(2016, 6, 1), y: 19.8 }, { x: new Date(2016, 7, 1), y: 18.1 },
              { x: new Date(2016, 8, 1), y: 13.1 }, { x: new Date(2016, 9, 1), y: 4.1 },
              { x: new Date(2016, 10, 1), y: -3.8 }, { x: new Date(2016, 11, 1), y: -6.8 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',valueType: 'DateTime',labelFormat: 'yMMM',
           edgeLabelPlacement: 'Shift',majorGridLines : { width : 0 } } }
           primaryYAxis={ {title: 'Profit ($)',rangePadding: 'None',lineStyle : { width: 0 },
           majorTickLines : {width : 0} } }
           legendSettings={ {visible:false} }
           zoomSettings={ {enableMouseWheelZooming: true,enablePinchZooming: true,
           enableSelectionZooming: true} }
           title='Sales History of Product X'>
    <Inject services={[AreaSeries, Legend, Tooltip, DataLabel,Zoom, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' opacity={0.6} name='Product X' type='Area'
         border={ { width: 0.5, color: '#00bdae' } } animation={ {enable: false} }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

After zooming the chart, a zooming toolbar will appear with `zoom`,`zoomin`, `zoomout`, `pan` and `reset` buttons.
Selecting the Pan option will allow to pan the chart and selecting the Reset option will reset the zoomed chart.

**Modes of Zooming**

The [`mode`](../api/chart/zoomSettingsModel/#mode) property in zoomSettings specifies whether the chart is allowed to scale along the horizontal axis or vertical axis. The default value of the mode is XY (both axis).

There are three types of mode.

* X - Allows us to zoom the chart horizontally.
* Y - Allows us to zoom the chart vertically.
* XY - Allows us to zoom the chart both vertically and horizontally.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries, Zoom}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
              { x: new Date(2016, 0, 1), y: 7.1 }, { x: new Date(2016, 1, 1), y: 3.7 },
              { x: new Date(2016, 2, 1), y: 0.8 }, { x: new Date(2016, 3, 1), y: 6.3 },
              { x: new Date(2016, 4, 1), y: 13.3 }, { x: new Date(2016, 5, 1), y: 18.0 },
              { x: new Date(2016, 6, 1), y: 19.8 }, { x: new Date(2016, 7, 1), y: 18.1 },
              { x: new Date(2016, 8, 1), y: 13.1 }, { x: new Date(2016, 9, 1), y: 4.1 },
              { x: new Date(2016, 10, 1), y: -3.8 }, { x: new Date(2016, 11, 1), y: -6.8 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',valueType: 'DateTime',labelFormat: 'yMMM',
           edgeLabelPlacement: 'Shift',majorGridLines : { width : 0 } } }
           primaryYAxis={ {title: 'Profit ($)',rangePadding: 'None',lineStyle : { width: 0 },
           majorTickLines : {width : 0} } }
           legendSettings={ {visible:false} }
           zoomSettings={ {mode: 'X', enableSelectionZooming: true} }
           title='Sales History of Product X'>
    <Inject services={[AreaSeries, Legend, Tooltip, DataLabel,Zoom, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' opacity={0.6} name='Product X' type='Area'
         border={ { width: 0.5, color: '#00bdae' } } animation={ {enable: false} }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Customizing Zooming Toolbar**

By default, zoomin, zoomout, pan and reset buttons will be displayed for zoomed chart. You can customize to show your desire tools in the toolbar using [`toolbarItems`](../api/chart/zoomSettingsModel/#toolbaritems) property.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, AreaSeries, Zoom}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
              { x: new Date(2016, 0, 1), y: 7.1 }, { x: new Date(2016, 1, 1), y: 3.7 },
              { x: new Date(2016, 2, 1), y: 0.8 }, { x: new Date(2016, 3, 1), y: 6.3 },
              { x: new Date(2016, 4, 1), y: 13.3 }, { x: new Date(2016, 5, 1), y: 18.0 },
              { x: new Date(2016, 6, 1), y: 19.8 }, { x: new Date(2016, 7, 1), y: 18.1 },
              { x: new Date(2016, 8, 1), y: 13.1 }, { x: new Date(2016, 9, 1), y: 4.1 },
              { x: new Date(2016, 10, 1), y: -3.8 }, { x: new Date(2016, 11, 1), y: -6.8 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',valueType: 'DateTime',labelFormat: 'yMMM',
           edgeLabelPlacement: 'Shift',majorGridLines : { width : 0 } } }
           primaryYAxis={ {title: 'Profit ($)',rangePadding: 'None',lineStyle : { width: 0 },
           majorTickLines : {width : 0} } }
           legendSettings={ {visible:false} }
           zoomSettings={ {enableSelectionZooming: true,  toolbarItems: ['Zoom', 'Pan', 'Reset']} }
           title='Sales History of Product X'>
    <Inject services={[AreaSeries, Legend, Tooltip, DataLabel,Zoom, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='Product X' opacity={0.6} type='Area'
         border={ { width: 0.5, color: '#00bdae' } } animation={ {enable: false} }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

>Note: To use zooming feature, we need to inject `Zoom` module into the `services`.

## Crosshair

Crosshair has a vertical and horizontal line to view the value of the axis at mouse or touch position.

To get start quickly with React Chart Crosshair, you can check on this video:

`youtube:gAMNG5ogCbE`

**Enable Crosshair**

Crosshair lines can be enabled by using [`enable`](../api/chart/crosshairSettings/#enable) property in the `crosshair`. Likewise tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltipModel/#enable) property of `crosshairTooltip` in the corresponding axis.



{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, LineSeries, Crosshair}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
              { x: new Date(2016, 0, 1), y: -7.1, y1: -3 }, { x: new Date(2016, 1, 1), y: -3.7, y1: -3 },
              { x: new Date(2016, 2, 1), y: 0.8, y1: 4 }, { x: new Date(2016, 3, 1), y: 6.3, y1: 15 },
              { x: new Date(2016, 4, 1), y: 13.3, y1: 15 }, { x: new Date(2016, 5, 1), y: 18.0, y1: 33 },
              { x: new Date(2016, 6, 1), y: 19.8, y1: 25 }, { x: new Date(2016, 7, 1), y: 18.1, y1: 18 },
              { x: new Date(2016, 8, 1), y: 13.1, y1: 16 }, { x: new Date(2016, 9, 1), y: 4.1, y1: 11 },
              { x: new Date(2016, 10, 1), y: -3.8, y1: 2 }, { x: new Date(2016, 11, 1), y: -6.8, y1: -3.3 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',valueType: 'DateTime',labelFormat: 'yMMM',
           edgeLabelPlacement: 'Shift',crosshairTooltip: { enable: true },
           majorGridLines : { width : 0 } } }
           primaryYAxis={ {title: 'Profit ($)',rangePadding: 'None',lineStyle : { width: 0 },
           majorTickLines : {width : 0}, crosshairTooltip: { enable: true },} }
           crosshair = { {enable:true} }
           title='Sales History of Product X'>
    <Inject services={[LineSeries, Legend, Tooltip, DataLabel,Crosshair, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='Product X' type='Line'
        marker={ {visible:true} } >
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Product X' type='Line'
        marker={ {visible:true} } >
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Customization**

The [`fill`](../api/chart/crosshairTooltipModel/#fill) and [`textStyle`](../api/chart/crosshairTooltipModel/#textstyle) property of the `crosshairTooltip` is used to customize the background color and font style of the crosshair label respectively.
Color and width of the crosshair line can be customized by using the [`line`](../api/chart/crosshairSettings/#line) property in the crosshair.

{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, LineSeries, Crosshair}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
              { x: new Date(2016, 0, 1), y: -7.1, y1: -3 }, { x: new Date(2016, 1, 1), y: -3.7, y1: -3 },
              { x: new Date(2016, 2, 1), y: 0.8, y1: 4 }, { x: new Date(2016, 3, 1), y: 6.3, y1: 15 },
              { x: new Date(2016, 4, 1), y: 13.3, y1: 15 }, { x: new Date(2016, 5, 1), y: 18.0, y1: 33 },
              { x: new Date(2016, 6, 1), y: 19.8, y1: 25 }, { x: new Date(2016, 7, 1), y: 18.1, y1: 18 },
              { x: new Date(2016, 8, 1), y: 13.1, y1: 16 }, { x: new Date(2016, 9, 1), y: 4.1, y1: 11 },
              { x: new Date(2016, 10, 1), y: -3.8, y1: 2 }, { x: new Date(2016, 11, 1), y: -6.8, y1: -3.3 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Years',valueType: 'DateTime',labelFormat: 'yMMM',
           edgeLabelPlacement: 'Shift',crosshairTooltip: { enable: true, fill: 'green' },
           majorGridLines : { width : 0 } } }
           primaryYAxis={ {title: 'Profit ($)',rangePadding: 'None',lineStyle : { width: 0 },
           majorTickLines : {width : 0}, crosshairTooltip: { enable: true, fill: 'green' } } }
           crosshair = { {enable:true, line:{width:2, color:'green'} } }
           title='Sales History of Product X'>
    <Inject services={[LineSeries, Legend, Tooltip, DataLabel,Crosshair, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='Product X' type='Line'
        marker={ {visible:true} } >
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Product X' type='Line'
        marker={ {visible:true} } >
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

>Note: To use crosshair feature, we need to inject `Crosshair` module into the `services`.

## Trackball

Trackball is used to track a data point closest to the mouse or touch position. Trackball marker indicates the closest point and trackball tooltip displays the information about the point. To use trackball feature, we need to inject `Crosshair` and `Tooltip` module into the `services`.

Trackball can be enabled by setting the [`enable`](../api/chart/crosshairSettings/#enable) property of the crosshair to true and
[`shared`](../api/chart/tooltipSettings/#shared) property in `tooltip` to true in chart.

{% tab template="chart/user-interaction/trackball", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, DateTime, Tooltip, DataLabel, LineSeries, Crosshair}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
            { x: new Date(2000, 2, 11), y: 15, y1: 39, y2: 60, y3: 75, y4: 85 },
            { x: new Date(2000, 9, 14), y: 20, y1: 30, y2: 55, y3: 75, y4: 83 },
            { x: new Date(2001, 2, 11), y: 25, y1: 28, y2: 48, y3: 68, y4: 85 },
            { x: new Date(2001, 9, 16), y: 21, y1: 35, y2: 57, y3: 75, y4: 87 },
            { x: new Date(2002, 2, 7), y: 13, y1: 39, y2: 62, y3: 71, y4: 82 },
            { x: new Date(2002, 9, 7), y: 18, y1: 41, y2: 64, y3: 69, y4: 74 },
            { x: new Date(2003, 2, 11), y: 24, y1: 45, y2: 57, y3: 81, y4: 73 },
            { x: new Date(2003, 9, 14), y: 23, y1: 48, y2: 53, y3: 84, y4: 75 },
            { x: new Date(2004, 2, 6), y: 19, y1: 54, y2: 63, y3: 85, y4: 73 },
            { x: new Date(2004, 9, 6), y: 31, y1: 55, y2: 50, y3: 87, y4: 60 },
            { x: new Date(2005, 2, 11), y: 39, y1: 57, y2: 66, y3: 75, y4: 48 },
            { x: new Date(2005, 9, 11), y: 50, y1: 60, y2: 65, y3: 70, y4: 55 },
            { x: new Date(2006, 2, 11), y: 24, y1: 60, y2: 79, y3: 85, y4: 40 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ { title: 'Years', minimum: new Date(2000, 1, 1),
           maximum: new Date(2006, 2, 11),intervalType: 'Years',valueType: 'DateTime',
           lineStyle: { width: 0 },majorGridLines: { width: 0 },edgeLabelPlacement: 'Shift'} }
           primaryYAxis={ {title: 'Revenue in Millions',labelFormat: '{value}M',
           majorTickLines: { width: 0 },minimum: 10, maximum: 90,lineStyle: { width: 0 } } }
           crosshair = { {enable: true, lineType: 'Vertical'} }
           tooltip={ { enable: true, shared: true, format: '${series.name} : ${point.x} : ${point.y}'} }
           title='Average Sales per Person'>
    <Inject services={[LineSeries, Legend, Tooltip, DataLabel,Crosshair, DateTime]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y' name='John' type='Line' width={2}
        marker={ {visible:true} } >
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y1' name='Andrew' type='Line' width={2}
        marker={ {visible:true} } ></SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y2' name='Thomas' type='Line' width={2}
        marker={ {visible:true} } ></SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y3' name='Mark' type='Line' width={2}
        marker={ {visible:true} } ></SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='x' yName='y4' name='William' type='Line' width={2}
        marker={ {visible:true} } ></SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

## Selection

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

**Point**

 You can select a point, by setting `selectionMode` to point.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',title: 'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals' selectionMode='Point'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel,Selection, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Series**

 You can select a series, by setting `selectionMode` to series.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',title: 'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals' selectionMode='Series'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel,Selection, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Cluster**

You can select the points that corresponds to the same index in all the series, by setting `selectionMode` to cluster.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',title: 'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals' selectionMode='Cluster'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel,Selection, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

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

export let data: any[] = [
              { height: 130, male: 35 , female: 32 },
              { height: 132, male: 38 , female: 33 },
              { height: 135, male: 41, female: 38 },
              { height: 137, male: 43 , female: 40 },
              { height: 140, male: 45, female: 42 },
              { height: 142, male: 46 , female: 42.5 },
              { height: 145, male: 48, female: 43 },
              { height: 147, male: 50 , female: 44 },
              { height: 150, male: 52, female: 45 },
              { height: 152, male: 55 , female: 45 },
              { height: 155, male: 58, female: 46 },
              { height: 157, male: 60 , female: 48 },
              { height: 160, male: 63, female: 51 },
              { height: 162, male: 70 , female: 54 },
              { height: 165, male: 75, female: 58 },
              { height: 167, male: 78 , female: 62 },
              { height: 170, male: 82, female: 68 },
              { height: 172, male: 87 , female: 72 },
              { height: 175, male: 89, female: 78 },
              { height: 177, male: 92 , female: 82 },
              { height: 180, male: 95, female:  85}
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {title: 'Height (cm)',minimum: 130, maximum: 180,
           edgeLabelPlacement: 'Shift',labelFormat: '{value}cm'} }
           primaryYAxis={ { title: 'Weight (kg)',minimum: 30, maximum: 100,
           labelFormat: '{value}kg', rangePadding: 'None'} }
           selectionMode='DragXY'
           title='Height Vs Weight'>
    <Inject services={[ScatterSeries, Legend, Tooltip, Selection]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='height' yName='male' name='Male' type='Scatter'
         marker={ {  width: 12, height: 12 } }>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='height' yName='female' name='Female' type='Scatter'
         marker={ {  width: 12, height: 12 } }>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Selection Type**

You can select multiple points or series, by enabling the [`isMultiSelect`](../api/chart/chartModel/#ismultiselect) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',title: 'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals' isMultiSelect={true} selectionMode='Point'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel,Selection, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'>
        </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'>
        </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Customizing Selection Style**

You can apply custom style to selected points or series with [`selectionStyle`](../api/chart/series/#selectionstyle) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];

ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',title: 'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals' isMultiSelect={true} selectionMode='Point'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel,Selection, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'
        selectionStyle='chartSelection1'>  </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'
        selectionStyle='chartSelection2'> </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'
        selectionStyle='chartSelection3'> </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

**Selection on Load**

You can able to select a point or series programmatically on a chart using [`selectedDataIndexes`](../api/chart/chartModel/#selecteddataindexes) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, Selection}
from'@syncfusion/ej2-react-charts';

export let data: any[] = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
export let selectedData: any[] = [ { series: 0, point: 1}, { series: 2, point: 3}];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',title: 'Countries'} }
           primaryYAxis={ { minimum: 0, maximum: 80,interval: 20, title: 'Medals'} }
           title='Olympic Medals' selectedDataIndexes ={selectedData}
            isMultiSelect={true} selectionMode='Point'>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Selection, Category]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='gold' name='Gold' type='Column'
        selectionStyle='chartSelection1' animation={ {enable:false} } >  </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='silver' name='Silver' type='Column'
        selectionStyle='chartSelection2' animation={ {enable:false} }> </SeriesDirective>
        <SeriesDirective dataSource ={data}  xName='country' yName='bronze' name='Bronze' type='Column'
        selectionStyle='chartSelection3' animation={ {enable:false} }> </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}

>Note: To use select feature, we need to Inject `Selection` module into the `services`.

## Data Editing

We can use the data editing through inject the `DataEditing` module in the chart. It provides drag and drop support to the rendered points. Now, we can change the location or value of the point based on its `y` value.  To enable the data editing, set the `enable` property to true in the drag settings of the series. Also, we can set color using `fill` property and set the data editing minimum and maximum range using `minY` and `maxY` properties.

{% tab template="chart/user-interaction/data-editing", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ChartComponent, SeriesCollectionDirective, SeriesDirective, Inject,
         Legend, Category, Tooltip, DataLabel, ColumnSeries, LineSeries, DataEditing}
from'@syncfusion/ej2-react-charts';

export let columnData: any[] = [
                { x: '2005', y: 21 }, { x: '2006', y: 60 },
                { x: '2007', y: 45 }, { x: '2008', y: 50 },
                { x: '2009', y: 74 }, { x: '2010', y: 65 },
                { x: '2011', y: 85 }
        ];
export let lineData: any[] = [
                { x: '2005', y: 21 }, { x: '2006', y: 22 },
                { x: '2007', y: 36 }, { x: '2008', y: 34 },
                { x: '2009', y: 54 }, { x: '2010', y: 55 },
                { x: '2011', y: 60 }
        ];
ReactDOM.render(
 <ChartComponent id='charts'
           primaryXAxis={ {  valueType: 'Category',
            minimum: -0.5,
            maximum: 6.5,
            labelPlacement: 'OnTicks',
            majorGridLines: { width: 0 } } }
            chartArea={{
            border: {
                width: 0
            }
            }}
           primaryYAxis={ { rangePadding: 'None',
            minimum: 0,
            title : 'Sales',
            labelFormat: '{value}%',
            maximum: 100,
            interval: 20,
            lineStyle: { width: 0 },
            majorTickLines: { width: 0 },
            minorTickLines: { width: 0 } } }
           title='Sales Prediction of Products'
           tooltip={{enable: true}}>
    <Inject services={[ColumnSeries, Legend, Tooltip, DataLabel, Category, LineSeries, DataEditing ]}/>
    <SeriesCollectionDirective>
        <SeriesDirective dataSource ={columnData}  xName='x' yName='y' name='Product A' type='Column' dragSetting={{enable: true}} marker={{visible: true, width: 10, height: 10}}>  </SeriesDirective>
        <SeriesDirective dataSource ={lineData}  xName='x' yName='y' name='Product B' type='Line' marker={{visible: true, width: 10, height: 10}} dragSettings={{enable: true}}> </SeriesDirective>
    </SeriesCollectionDirective>
  </ChartComponent>, document.getElementById('charts')
);

```

{% endtab %}
