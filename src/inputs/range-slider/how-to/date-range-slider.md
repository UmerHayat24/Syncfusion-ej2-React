# Date range slider

The Date formatting can be achieved in `ticks` and `tooltip` using `renderingTicks` and `tooltipChange` events respectively. The process
of formatting is explained in the below sample.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public min = new Date("2013-06-13").getTime();
  public max = new Date("2013-06-21").getTime();
  public step = 86400000;
  public value = new Date("2013-06-15").getTime();

  // Slider ticks customization
  public ticks: TicksDataModel = { placement: "After", largeStep: 2 * 86400000 };
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true };

  renderingTicksHandler(args: SliderTickEventArgs) {
    let totalMiliSeconds = Number(args.value);
    // Converting the current milliseconds to the respective date in desired format
    let custom = { year: "numeric", month: "short", day: "numeric" };
    args.text = new Date(totalMiliSeconds).toLocaleDateString("en-us", custom);
  }

  tooltipChangeHandler(args: SliderTooltipEventArgs) {
    let totalMiliSeconds = Number(args.text);
    // Converting the current milliseconds to the respective date in desired format
    let custom = { year: "numeric", month: "short", day: "numeric" };
    args.text = new Date(totalMiliSeconds).toLocaleDateString("en-us", custom);
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
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
