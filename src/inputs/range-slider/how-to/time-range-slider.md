# Time range slider

The time formatting can be achieved same as the date formatting using `renderingTicks` and `change` events. The process of time formatting is
explained in the below sample.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public min = new Date(2013, 6, 13, 11).getTime();
  public max = new Date(2013, 6, 13, 17).getTime();
  public value = new Date(2013, 6, 13, 13).getTime();
  public step = 3600000;

  // Slider ticks customization
  public ticks: TicksDataModel = { placement: "After", largeStep: 2 * 3600000 };
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true };

  renderingTicksHandler(args: SliderTickEventArgs) {
    let totalMiliSeconds = Number(args.value);
    let custom = { hour: "2-digit", minute: "2-digit" };
    args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
  }

  tooltipChangeHandler(args: SliderTooltipEventArgs) {
    let totalMiliSeconds = Number(args.text);
    let custom = { hour: "2-digit", minute: "2-digit" };
    args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
  }

  render() {
    return (
      <div id="container">
        <div className="wrap">
          <SliderComponent
            id="slider"
            min={this.min}
            max={this.max}
            value={this.value}
            step={this.step}
            tooltip={this.tooltip}
            ticks={this.ticks}
            showButtons={true}
            tooltipChange={this.tooltipChangeHandler.bind(this) as any}
            renderingTicks={this.renderingTicksHandler.bind(this) as any}
          />
        </div>
      </div>
    );
  }}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
