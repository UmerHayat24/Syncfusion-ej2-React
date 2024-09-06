# Title and Subtitle

## Enable title

The title and subtitle are used to describe the information about the data being plotted in the Smith chart. You can set the title and subtitle of the Smith chart using the [`text`] property. By default, the visibility of the title and subtitle is enabled. The following code sample demonstrates how to simply set text to title and subtitle.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.title.text = 'Impedance Transmission';
        args.smithchart.title.visible = true;
        args.smithchart.title.subtitle.text = 'Transmission';
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

## Trim title

Both the title and subtitle of the Smith chart can be trimmed if they exceed the certain length. Trimming is enabled using the [`enableTrim`] property for title and subtitle. The length for title and subtitle can be changed using the [`maximumWidth`] property. You can also customize the font, alignment, and visibility of title and subtitle using the [`font`], [`textAlignment`], and [`visibility`] properties.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { SmithchartComponent, SmithchartSeriesCollectionDirective, SmithchartSeriesDirective } from '@syncfusion/ej2-react-charts';

class App extends React.Component {
    public load(args: ISmithchartLoadedEventArgs): void {
        args.smithchart.title.text = 'Impedance Transmission';
        args.smithchart.title.visible = true;
        args.smithchart.title.subtitle.text = 'Transmission';
        args.smithchart.title.enableTrim = true;
        args.smithchart.title.maximumWidth = 70;
        args.smithchart.title.subtitle.textAlignment = 'Far';
        args.smithchart.title.subtitle.enableTrim = true;
        args.smithchart.title.subtitle.maximumWidth = 40;
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