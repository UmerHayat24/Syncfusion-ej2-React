# Numeric range slider

The numeric values can be formatted into different decimal digits or fixed number of whole numbers or to represent the units. The Numeric
processing is demonstrated below.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  // Slider ticks customization
  public ticks01: TicksDataModel = {
    placement: "After",
    format: "##.## Km",
    largeStep: 20,
    smallStep: 10,
    showSmallTicks: true
  };
  public tooltip01: TooltipDataModel = { isVisible: true, format: "##.## Km" };

  public ticks02: TicksDataModel = {
    placement: "After",
    format: "##.#00",
    largeStep: 0.02,
    smallStep: 0.01,
    showSmallTicks: true
  };
  public tooltip02: TooltipDataModel = { isVisible: true, format: "##.#00" };

  public tooltip03: TooltipDataModel = { isVisible: true, format: "00##" };
  public ticks03: TicksDataModel = {
    placement: "After",
    format: "00##",
    largeStep: 20,
    smallStep: 10,
    showSmallTicks: true
  };

  render() {
    return (
      <div id="container">
        <div className="wrap">
          <div className="label">Slider formatted with unit representation</div>
          <SliderComponent
            id="slider"
            min={0}
            max={100}
            value={30}
            step={1}
            tooltip={this.tooltip01}
            ticks={this.ticks01}
          />
        </div>

        <div className="wrap">
          <div className="label">Slider formatted with three decimal specifiers</div>
          <SliderComponent
            id="slider1"
            min={0.1}
            max={0.2}
            value={0.13}
            step={0.01}
            tooltip={this.tooltip02}
            ticks={this.ticks02}
          />
        </div>

        <div className="wrap">
          <div className="label">Slider formatted with two leading zeros</div>
          <SliderComponent
            id="slider2"
            min={0}
            max={100}
            value={30}
            step={1}
            tooltip={this.tooltip03}
            ticks={this.ticks03}
          />
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
