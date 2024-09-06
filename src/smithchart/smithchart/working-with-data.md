# Working with Data

The Smith chart can visualize the data bound from local data. The data bound for the Smith chart should be an array of object and should contain the field resistance and rectangle. This data should be bound to points or data source in the Smith chart.

## Data Binding

You can bind simple JSON data to Smith chart using the point property in series. The JSON data should contain [`resistance`] and [`reactance`] fields. This JSON data should be bound to points or data source in the Smith chart. You can add any number of JSON or data source to points.

{% tab template= "smithchart/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx", isDefaultActive=true , es5Template = "es5default" %}

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