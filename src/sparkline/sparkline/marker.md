# Markers

This section explains how to add markers to the sparkline.

## Adding marker to the sparkline

To add marker to the sparkline, specify the `visible` of `markerSettings` as following values. The `visible` will accept multiple values too.

* All - Enables markers for all points.
* Start - Enables marker for the start point.
* End - Enables marker for the end point.
* High - Enables marker for the high point.
* Low - Enables marker for the low point.
* Negative - Enables markers for the negative points.

The following code example shows enabling markers for all points.

{% tab template= "sparkline/marker", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Marker" %}

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
    dataSource= { [0, 6, 4, 1, 3, 2, 5] }
    // To enable markers for all points
    markerSettings= { {
        visible: ['All']
    } }>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Adding marker to special point

In sparkline, markers can be enabled for particular points such as the start, end, low, high, or negative. The following code examples shows enabling markers for the high and low points.

{% tab template= "sparkline/marker", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Marker" %}

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
    dataSource= { [3, 6, 4, 1, 3, 2, 5] }
    // To enable marker for high and low points with color customization
    highPointColor= 'blue'
    lowPointColor= 'red'
    markerSettings= { {
        visible: ['High', 'Low']
    } }>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Customizing markers

Sparkline markers can be customized in terms of fill color, border color, width, opacity, and size. The following code example shows customizing marker's fill, border, and size.

{% tab template= "sparkline/marker", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Marker" %}

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
    dataSource= { [3, 6, 4, 1, 3, 2, 5] }
    // To enable marker for high and low points with color customization
    fill= 'blue'
    markerSettings= { {
        visible: ['All'],
        size: 5, fill: 'white', border: { color: 'blue', width: 2}
    } }>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}