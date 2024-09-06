# User interactions

Sparkline has two user interaction features: tooltip and tracker line.

## Tooltip

The sparkline provides options to display details about values of data points through tooltips when hovering the mouse over data point. To use tooltip in sparkline, inject the `SparklineTooltip` module to sparkline using the inject method.

The following code example shows enabling tooltip for sparkline with format.

{% tab template= "sparkline/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Tooltip" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='500px'
    axisSettings= { {
        minX: -1, maxX: 7, maxY: 8, minY: -1
    } }
    fill= 'blue'
    valueType= 'Category'
    xName= 'x' yName= 'y'
    dataSource= { [
        {x: 'Mon', y: 3 },
        {x: 'Tue', y: 5 },
        {x: 'Wed', y: 2 },
        {x: 'Thu', y: 4 },
        {x: 'Fri', y: 6 },
    ] }
    // To enable tooltip for sparkline
    tooltipSettings= { {
        visible: true,
        // formatting tooltip text
        format: '${x} : ${y}'
    } }>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

### Tooltip customization

The fill color, text styles, format, and border of the tooltip can be customized. The following code example shows customization of tooltip's fill color and text style.

{% tab template= "sparkline/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Tooltip" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='500px'
    axisSettings= { {
        minX: -1, maxX: 7, maxY: 8, minY: -1
    } }
    fill= '#033e96'
    valueType= 'Category'
    xName= 'x' yName= 'y'
    dataSource= { [
        {x: 'Mon', y: 3 },
        {x: 'Tue', y: 5 },
        {x: 'Wed', y: 2 },
        {x: 'Thu', y: 4 },
        {x: 'Fri', y: 6 },
    ] }
    // To enable tooltip for sparkline with fill color customization
    tooltipSettings= { {
        visible: true,
        format: '${x} : ${y}',
        fill: '#033e96',
        textStyle: {
            color: 'white'
        },
    } }>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

### Tooltip template

Sparkline tooltip has template support. By using tooltip template, you can customize tooltips. The following code example shows more customization options provided to  `sparktooltip` css class that is used in tooltip template div. Using this template, images also can be added to tooltip.

{% tab template= "sparkline/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Tooltip" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='500px'
    axisSettings= { {
        minX: -1, maxX: 7, maxY: 8, minY: -1
    } }
    fill= '#033e96'
    valueType= 'Category'
    xName= 'x' yName= 'y'
    dataSource= { [
        {x: 'Mon', y: 3 },
        {x: 'Tue', y: 5 },
        {x: 'Wed', y: 2 },
        {x: 'Thu', y: 4 },
        {x: 'Fri', y: 6 },
    ] }
    // To enable tooltip template for sparkline with fill color, border radius and padding customization
    tooltipSettings= { {
        visible: true,
        template: '<div id="sparktooltip" style="border-radius: 5px;background: #008cff;' +
            'color: #FFFFFF !important;font-size: 16px;font-style: italic;padding: 8px;">' +
            '${x} : ${y} </div>'
    } }>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Track line

The track line tracks data points that are closer to the mouse position or touch contact.

To enable track lines for sparkline, specify the `visible` option of  `trackLineSettings` to true. Based on theme, tracker color will be changed. The default value of tracker color is black.

To use track line in sparkline, inject the `SparklineTooltip` module to sparkline using the inject method.

{% tab template= "sparkline/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Tooltip" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='500px'
    axisSettings= { {
        minX: -1, maxX: 46, maxY: 10, minY: -1
    } }
    fill= '#033e96'
    dataSource= { [5, 3, 4, 6, 8, 7, 9, 1, 3, 5, 3, 4, 6, 8, 7, 9, 1, 3, 5, 2, 4, 6, 7, 9, 5, 8, 3, 6, 1, 7, 4, 2, 5, 2, 4, 6, 7, 9, 5, 8, 3, 6, 1, 7, 4, 2] }
    // To enable tooltip template for sparkline with fill color, border radius and padding customization
    tooltipSettings= { {
        trackLineSettings: {
            visible: true,
            color: '#033e96',
            width: 1
        }
    } }>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}