<!-- markdownlint-disable MD036 -->

# Markers and Data labels

The markers and data labels are used to provide information about the data points in the series. You can add a shape to adorn each data point. By default, both the marker and data label are disabled in Smith chart. You can enable them by setting the visible property to true in marker and data label settings.

## Marker

By default, the visibility of marker is false. You can enable marker by setting the visible property to true in marker settings. Using marker settings, you can customize marker differently for each series in Smith chart.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective, TooltipRender } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
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

### Marker customization

Using marker settings in series, you can customize the marker for each series differently. You can customize the markers using the following properties differently for each series in the Smith chart:

* [`width`]: Controls the width of the marker.
* [`height`]: Controls the height of the marker.
* [`fill`]: Customizes the fill color of the marker.
* [`opacity`]: Customizes the opacity of the marker.
* [`border`]: Controls the width and color of the marker's border.
* [`shape`]: Changes the shape of the marker.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective, TooltipRender } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.series[0].marker = {
            visible: true,
            height: 10,
            width: 10,
            fill: '#ff99ff',
            opacity: 1,
            shape: 'rectangle',
            border: {
                color: '#cc00cc',
                width: 2
            }
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

## Data labels

By default, the data labels are disabled. You can enable the data labels by setting the visible property to true in data label settings. For each point in series, a data label is created. The data labels for each series can be customized differently using the data label settings.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx",isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective, TooltipRender } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.series[0].marker = {
            dataLabel: {
                visible: true
            }
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

### Data label customization

Using data label settings in marker, you can customize the data label for each series differently. The following properties are used to customize data labels differently for each series:

* [`fill`]: Changes the fill color of the data label's shape.
* [`opacity`]: Controls the opacity of the data label's shape.
* [`border`]: Customizes the width and color of the border.
* [`textStyle`]: Customizes the font color, width, and size.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective, TooltipRender } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.series[0].marker = {
            dataLabel: {
                visible: true,
                fill: '#99ffcc',
                opacity: 1,
                border: {
                    color: '#1aff8c',
                    width: 2,
                }
            }
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