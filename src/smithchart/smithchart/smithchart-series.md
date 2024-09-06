# Series

You can add any number of series to Smith chart as needed. By using the series setting, you can add or customize the data. For the points and data source added in the series, line can be drawn. You can customize the each series with marker, data label, animation, opacity, and so on.

## points or data source

For adding values in the Smith chart, you can use either points or data source in the series. Both the points and data source should be an array of object, which should contain the field names resistance and rectangle.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx",isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
render() {
  return ( <SmithchartComponent id='smithchart'>
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

## Series customization

Using the following options in series settings, you can customize the each series in Smith chart:

* [`fill`]: Customizes the fill color for the series.
* [`enableSmartLabels`]: Places the data labels on Smith chart without overlapping with each other.
* [`visibility`]: Handles the visibility of the series.
* [`opacity`]: Controls the opacity of the series line.
* [`width`]: Customizes the width of the series line.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.series[0].fill = '#009933';
        args.smithchart.series[0].visibility = 'visible';
        args.smithchart.series[0].opacity = 0.75;
        args.smithchart.series[0].width = 2.5
        args.smithchart.series[0].marker= { dataLabel: { visible: true }};
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
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