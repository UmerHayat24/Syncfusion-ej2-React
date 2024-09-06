# Tooltip

The Smith chart displays details about the points using tooltip when the mouse is hovered over the points. By default, the tooltips are disabled. To enable the tooltips, import and inject the TooltipRender module from Smith chart, and set the visible property to true in tooltip settings. You can customize the visibility and appearance of tooltips for each series in the Smith chart.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective, TooltipRender } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.series[0].tooltip = {
            visible: true
        };
        args.smithchart.series[0].marker = {
            visible: true
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[TooltipRender]} />
                        <SmithchartSeriesCollectionDirective>
                            <SmithchartSeriesDirective
                                points={[
                                    { resistance: 10, reactance: 25 }, { resistance: 8, reactance: 6 },
                                    { resistance: 6, reactance: 4.5 }, { resistance: 4.5, reactance: 2 },
                                    { resistance: 3.5, reactance: 1.6 }, { resistance: 2.5, reactance: 1.3 },
                                    { resistance: 2, reactance: 1.2 }, { resistance: 1.5, reactance: 1 },
                                    { resistance: 1, reactance: 0.8 }, { resistance: 0.5, reactance: 0.4 },
                                    { resistance: 0.3, reactance: 0.2 }, { resistance: 0, reactance: 0.15 },
                                ]} name='Transmission1'
                                >
                            </SmithchartSeriesDirective>
                        </SmithchartSeriesCollectionDirective>
            </SmithchartComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('smithchart'));

```

{% endtab %}
