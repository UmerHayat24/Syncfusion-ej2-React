# Localization

The sparkline control supports localization. The default culture for localization is `en-US`. You can change the culture using the `setCulture` method.

## Tooltip format

Sparkline tooltip supports localization. The following code sample shows tooltip text with currency format based on culture.

{% tab template="sparkline/localization", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true,  es5Template="es5Localization" %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SparklineComponent, Inject, SparklineTooltip } from '@syncfusion/ej2-react-charts';

export class App extends React.Component {
render() {
  return ( <SparklineComponent id='sparkline'
    height='200px' width='350px'
    containerArea= { {
        border: { color: '#033e96', width: 2 }
    } }
    tooltipSettings= { {
        visible: true
    } }
    // To specify currency format
    format= { "c0" }
    useGroupingSeparator= { true }
    lineWidth= { 3 }
    padding= { { left: 20, right: 20, bottom: 20, top: 20} }
    border= { { color: '#033e96', width: 2 } }
    type= 'Area'
    fill= '#b2cfff'
    dataSource= { [30000, 60000, 40000, 10000, 30000, 20000, 50000] }>
    <Inject services={[SparklineTooltip]} />
</SparklineComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('sparkline'));
```

{% endtab %}