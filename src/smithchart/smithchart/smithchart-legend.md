<!-- markdownlint-disable MD036 -->

# Legend

Legend is a key used in smithchart; it contains symbols and descriptions. The legends provide a valuable information for interpreting what the Smith chart displays. They can be represented in various colors, shapes, or other identifiers based on the data. The legends are used to denote the series rendered in the Smith chart.

## Position and alignment

### Position

By default, the visibility of the legend is false. To enable the legend, set the visible property to true in legendSettings. The default position for the legend is bottom. By using the [`position`] property, you can either place the legend at the bottom, top, right, or left of the Smith chart. To use the legend in Smith chart, import and inject the SmithchartLegend from chart.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            visible: true,
            position: 'Top'
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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

#### Custom position

The legends are not limited to place at the default positions only. You can place a legend anywhere in the Smith chart by setting the position as custom in legendSettings and specifying the x and y-coordinates using the x and y properties.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            position: 'Custom',
            location:{
                x: 80,
                y: 100
            }
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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

### Legend alignment

By default, the legends are aligned in center position. Using the [`alignment`] property, you can align the legend in near and far locations of the Smith chart.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            visible: true,
            position: 'Top',
            alignment: 'Near'
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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

## Customization

### Legend shape

By default, the legends are rendered in a circle shape. The color of the shape will be same as the series color. Using the [`shape`] property in legend settings, you can change the shape of the legend to rectangle, triangle, and so on.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            visible: true,
            position: 'Top',
            shape: 'Rectangle'
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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

### Legend size

By default, a legend takes 20 to 25% of the chart's height horizontally when it is placed at the top or bottom position and 20 to 25% of the width vertically when placing at the left or right. You can change the legend size using the [`width`] and [`height`] properties of the legendSettings.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            visible: true,
            position: 'Top',
            height: 100,
            width: 200
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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

### Padding

You can customize the space between two legend items and space between legend shape and text as needed. For customizing the space between two legend items, use the [`itemPadding`] property. To control the space between legend shape and text, use the [`shapePadding`] property.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx",isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            visible: true,
            position: 'Top',
            itemPadding: 5,
            shapePadding: 10
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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

## Toggle visibility

By default, the series name is displayed in the legend. You can collapse the visibility of a series by clicking the legend for the particular series and toggle the series visibility to true or false using the [`toggleVisibility`] property. By default, this property is set to true.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Inject, SmithchartComponent, SmithchartLegend, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.legendSettings = {
            visible: true,
            position: 'Top',
            toggleVisibility: false
        };
    }
render() {
  return ( <SmithchartComponent id='smithchart' load={this.load.bind(this)}>
                <Inject services={[SmithchartLegend]} />
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