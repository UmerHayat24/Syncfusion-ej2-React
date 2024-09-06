# Data Labels

Data labels are used to display values of data points to improve the readability.

## Enable data label

To enable data label for sparkline series, provide `visible` of the `dataLabelSettings` as following possible values:

* All - Enables data label of  all points.
* Start - Enables data label of the start point.
* End - Enables data label of the end point.
* High - Enables data label of the high point.
* Low - Enables data label of the low point.
* Negative - Enables data labels of the negative points.

The following example shows enabling sparkline data label for all points.

{% tab template= "sparkline/datalabel", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Datalabel" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    axisSettings= { {
        minX: -1, maxX: 7, maxY: 7, minY: -1
    } }
    fill= 'blue'
    dataSource= { [ 0, 6, 4, 1, 3, 2, 5 ] }
    // To enable data label for all points
    dataLabelSettings= { {
        visible: ['All']
    } }>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Customize data label

Data labels can be customized using the fill, border, opacity, and textStyle. The following code example shows customizing data label border, text color, and fill color.

{% tab template= "sparkline/datalabel", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Datalabel" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    axisSettings= { {
        minX: -1, maxX: 7, maxY: 7, minY: -1
    } }
    fill= 'blue'
    dataSource= { [ 0, 6, 4, 1, 3, 2, 5 ] }
    // To customize data label fill, border, and text color
    dataLabelSettings= { {
        visible: ['All'],
        border: { color: 'blue', width: 1},
        fill: 'blue', opacity: 0.4,
        textStyle: {
            color: 'white'
        }
    } }>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Format data label text

The text of data labels can be formatted using the `format` API in the sparkline `dataLabelSettings`. By default, data label shows the y-value of point. The following code example shows how to display x and y-values for points.

{% tab template= "sparkline/datalabel", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Datalabel" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='500px'
    axisSettings= { {
        minX: -1, maxX: 7, maxY: 7, minY: -1
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
    // To enable data label for all points
    dataLabelSettings= { {
        format: '${x} : ${y}',
        visible: ['All'],
        border: { color: 'blue', width: 1},
        fill: 'blue', opacity: 0.4,
        textStyle: {
            color: 'white'
        }
    } }>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}