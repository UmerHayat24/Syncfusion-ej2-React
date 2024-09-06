# Axis

Like chart, Smith chart also has support for two types of axis:

* Horizontal axis: Axis drawn as straight line in horizontal direction of the chart.
* Radial axis: Axis drawn as circular path.

## Labels customization

Axis labels are used to denote the kind of data that is bound to Smith chart. Using axis labels, you can easily identify the interval, in which the chart is rendered. The following properties are used to customize the axis labels for horizontal and radial axes:

* [`labelPosition`]: Places the labels either inside or outside the axis line.
* [`labelIntersectAction`]: Hides the labels when intersect with other labels.
* [`labelStyle`]: Customizes the properties such as font size, family, weight, and opacity.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.radialAxis = {
            labelPosition: 'Inside',
            labelIntersectAction: 'Hide',
            labelStyle: {
                fontFamily: 'Times New Roman',
                fontWeight: 'bold',
                fontStyle: 'Italic',
                opacity: 0.75,
                size: '14px'
            }
        };
        args.smithchart.horizontalAxis = {
            labelPosition: 'Inside',
            labelIntersectAction: 'Hide',
            labelStyle: {
                fontFamily: 'Times New Roman',
                fontWeight: 'bold',
                fontStyle: 'Italic',
                opacity: 0.75,
                size: '14px'
            }
        };
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
                            <SmithchartSeriesDirective
                                points={[
                                    { resistance: 20, reactance: -50 }, { resistance: 10, reactance: -10 },
                                    { resistance: 9, reactance: -4.5 }, { resistance: 8, reactance: -3.5 },
                                    { resistance: 7, reactance: -2.5 }, { resistance: 6, reactance: -1.5 },
                                    { resistance: 5, reactance: -1 }, { resistance: 4.5, reactance: -0.5 },
                                    { resistance: 3.5, reactance: 0 }, { resistance: 2.5, reactance: 0.4 },
                                    { resistance: 2, reactance: 0.5 }, { resistance: 1.5, reactance: 0.5 },
                                    { resistance: 1, reactance: 0.4 }, { resistance: 0.5, reactance: 0.2 },
                                    { resistance: 0.3, reactance: 0.1 }, { resistance: 0, reactance: 0.05 },
                                ]} name='Transmission2'
                            >
                            </SmithchartSeriesDirective>
                        </SmithchartSeriesCollectionDirective>
            </SmithchartComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('smithchart'));

```

{% endtab %}

## Gridlines

To make the data easier to read in a chart that displays axes, display horizontal axis and radial axis gridlines. Gridlines are extended from any horizontal axis or radial axis across the plot area of the Smith chart.
Both horizontal and radial axes have support for major and minor gridlines. Major gridlines are drawn from the position in which labels are rendered. Minor gridlines are drawn between two major gridlines as per the count you set in settings.

You can customize the major and minor gridlines using the following properties:

* [`width`]: Customizes the width of gridlines.
* [`dashArray`]: Decides whether the gridlines have to be rendered as normal line or dashed line.
* [`visible`]: Enables or disables the visibility of the gridlines.
* [`opacity`]: Customizes the opacity of the major gridlines.
* [`count`]: Customizes the count of the minor gridlines.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.horizontalAxis = {
            majorGridLines: {
                visible: true,
                opacity: 0.8,
                width: 10
            }
        };
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
                            <SmithchartSeriesDirective
                                points={[
                                    { resistance: 20, reactance: -50 }, { resistance: 10, reactance: -10 },
                                    { resistance: 9, reactance: -4.5 }, { resistance: 8, reactance: -3.5 },
                                    { resistance: 7, reactance: -2.5 }, { resistance: 6, reactance: -1.5 },
                                    { resistance: 5, reactance: -1 }, { resistance: 4.5, reactance: -0.5 },
                                    { resistance: 3.5, reactance: 0 }, { resistance: 2.5, reactance: 0.4 },
                                    { resistance: 2, reactance: 0.5 }, { resistance: 1.5, reactance: 0.5 },
                                    { resistance: 1, reactance: 0.4 }, { resistance: 0.5, reactance: 0.2 },
                                    { resistance: 0.3, reactance: 0.1 }, { resistance: 0, reactance: 0.05 },
                                ]} name='Transmission2'
                            >
                            </SmithchartSeriesDirective>
                        </SmithchartSeriesCollectionDirective>
            </SmithchartComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('smithchart'));

```

{% endtab %}

## Axis line

Axis line is a line in Smith chart that can be configured to denote the axis. You can customize the axis line using the following properties:

* [`width`]: Customize the width of the axis line.
* [`dashArray`]: Renders the axis line as dashed line.
* [`visible`]: Enables or disable the visibility of the axis line.

By default, visibility of the axis line is true. You can customize its visibility by using the visible property in axis line.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.horizontalAxis = {
            majorGridLines: {
                visible: true,
                opacity: 0.8,
                width: 10
            },
            axisLine: {
                width: 10,
                visible: false
            }
        };
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
                            <SmithchartSeriesDirective
                                points={[
                                    { resistance: 20, reactance: -50 }, { resistance: 10, reactance: -10 },
                                    { resistance: 9, reactance: -4.5 }, { resistance: 8, reactance: -3.5 },
                                    { resistance: 7, reactance: -2.5 }, { resistance: 6, reactance: -1.5 },
                                    { resistance: 5, reactance: -1 }, { resistance: 4.5, reactance: -0.5 },
                                    { resistance: 3.5, reactance: 0 }, { resistance: 2.5, reactance: 0.4 },
                                    { resistance: 2, reactance: 0.5 }, { resistance: 1.5, reactance: 0.5 },
                                    { resistance: 1, reactance: 0.4 }, { resistance: 0.5, reactance: 0.2 },
                                    { resistance: 0.3, reactance: 0.1 }, { resistance: 0, reactance: 0.05 },
                                ]} name='Transmission2'
                            >
                            </SmithchartSeriesDirective>
                        </SmithchartSeriesCollectionDirective>
            </SmithchartComponent> );
 }
}
ReactDOM.render(<App />, document.getElementById('smithchart'));

```

{% endtab %}