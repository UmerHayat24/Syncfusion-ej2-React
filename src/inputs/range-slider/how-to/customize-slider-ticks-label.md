# Customize slider ticks label

Slider view can be customized via CSS. By overriding the slider CSS classes, you can customize the ticks. The ticks in slider allows you to easily identify the current value/values of the slider. It contains [`smallStep`](https://ej2.syncfusion.com/documentation/slider/api-ticksData.html?lang=typescript#smallstep) and [`largeStep`](https://ej2.syncfusion.com/documentation/slider/api-ticksData.html?lang=typescript#largestep). By default, slider has class `e-tick` for slider ticks. You can override the class as per your requirement. Refer to the following code snippet to render ticks.

```css
.e-scale .e-tick.e-custom::before {
    content: '\e967';
    position: absolute;
}
```

```css
#ticks_slider .e-scale :nth-child(1)::before {
    color: red;
}
```

Here, the color for rendered ticks has been applied through nth-child(`child_number`). The color is applied to the value of the `child_number` in the slider.

{% tab template="slider/ticks-custom", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent, SliderTickRenderedEventArgs, SliderTickEventArgs } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  private value: number[] = [30, 70];

  private icon: TicksDataModel = { placement: "Before", largeStep: 20 };

  private custom: TicksDataModel = { placement: "Both", largeStep: 20, smallStep: 5 };

  private iconTicks(args: SliderTickEventArgs): void {
    if (args.tickElement.classList.contains("e-large")) {
      args.tickElement.classList.add("e-custom");
    }
  }

  private customTicks(args: SliderTickRenderedEventArgs): void {
    let li: any = args.ticksWrapper.getElementsByClassName("e-large");
    let remarks: any = ["Very Poor", "Poor", "Average", "Good", "Very Good", "Excellent"];
    for (let i: number = 0; i < li.length; ++i) {
      (li[i].querySelectorAll(".e-tick-both")[1] as HTMLElement).innerText = remarks[i];
    }
  }

  render() {
    return (
      <div id="container">
        <div className="col-lg-12 control-section">
          <div className="slider-content-wrapper">
            <div className="slider_container" id="slider_wrapper">
              <div className="slider_labelText userselect">Dynamic ticks color</div>
              <SliderComponent
                id="ticks_slider"
                type="MinRange"
                min={0}
                max={100}
                step={5}
                value={30}
                ticks={this.icon}
                renderingTicks={this.iconTicks.bind(this) as any}
              />
            </div>

            <div className="slider_container">
              <div className="slider_labelText userselect">Ticks with legends</div>
              <SliderComponent
                id="slider"
                type="MinRange"
                min={0}
                max={100}
                value={this.value}
                ticks={this.custom}
                renderedTicks={this.customTicks.bind(this) as any}
              />
            </div>
          </div>
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
