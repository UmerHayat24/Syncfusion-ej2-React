# Appearance

The appearance of the sparkline can be customized using margin, container Area border, and container Area background.

## Sparkline border

The `containerArea border` of the sparkline is used to render border to cover sparkline area.

The following code example shows the sparkline with overall border.

{% tab template= "sparkline/appearance",sourceFiles="app/**/*.tsx", isDefaultActive=true , compileJsx=true,  es5Template="es5Appearance" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    containerArea= { {
        border: { color: '#033e96', width: 2 }
    }}
    border= { {
        color: '#033e96', width: 1
    }}
    type= 'Area'
    fill= '#b2cfff'
    dataSource={[ 3, 6, 4, 1, 3, 2, 5]}>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Sparkline padding

Padding is used to specify padding value between container and sparkline. By default, padding value of the sparkline is 5. Sparkline `padding` values are specified by the left, right, top, and bottom.

The following code example shows the sparkline with overall padding is set to 20.

{% tab template= "sparkline/appearance", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Appearance" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    containerArea= { {
        border: { color: '#033e96', width: 2 }
    }}
    // To render sparkline with padding
    padding= { { left: 20, right: 20, bottom: 20, top: 20} }
    border= { {
        color: '#033e96', width: 1
    }}
    type= 'Area'
    fill= '#b2cfff'
    dataSource={[ 3, 6, 4, 1, 3, 2, 5]}>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Sparkline area customization

The background color of the sparkline area can be customized using the `containerArea background` color. By default, the sparkline background color is `transparent`.

{% tab template= "sparkline/appearance", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Appearance" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    containerArea= { {
        border: { color: '#033e96', width: 2 },
        // To render sparkline with background
        background: '#eff1f4',
    }}
    padding= { { left: 20, right: 20, bottom: 20, top: 20} }
    border= { {
        color: '#033e96', width: 1
    }}
    type= 'Area'
    fill= '#b2cfff'
    dataSource={[ 3, 6, 4, 1, 3, 2, 5]}>
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}

## Sparkline theme

Datalabel and track line colors of the sparkline will be changed based on theme. For example, for dark theme, the color of datalabel and track line should be white; for light theme, their value should be black. The possible values for sparkline theme are `Material`, `Fabric`, `Bootstrap`, and `Highcontrast`.

The following code example shows the color for datalabel and track line is set to white for dark theme.

{% tab template= "sparkline/appearance", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true ,  es5Template="es5Appearance" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    // To specify theme
    theme= 'Highcontrast'
    dataLabelSettings= { { visible: ['All'] }}
    tooltipSettings= { {
        trackLineSettings: { visible: true }
    }}
    axisSettings= { {
        minX: -1, maxX: 7
    }}
    lineWidth= { 3 }
    border= { {
        color: 'transparent', width: 2
    }}
    type= 'Line'
    fill= '#007dd1'
    dataSource={[ 3, 6, 4, 1, 3, 2, 5]}>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}