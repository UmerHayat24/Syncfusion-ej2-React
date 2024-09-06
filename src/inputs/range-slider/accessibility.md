---
title: "Slider Accessibility"
component: "Slider"
description: "React slider component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

The Slider is characterized with complete ARIA Accessibility support that helps to access
by on-screen readers and other assistive technology devices. This component is designed with the
reference of guidelines document given in the [WAI ARAI Accessibility Practices](https://www.w3.org/TR/wai-aria-practices/#slider).

The Slider component uses the `Slider` role and the following ARIA properties for its element based on the state.

| **Property** | **Functionalities** |
| --- | --- |
| aria-valuenow | It Indicates the current value of the slider. |
| aria-valuetext | Returns the current text of the slider. |
| aria-valuemin | It Indicates the Minimum value of the slider. |
| aria-valuemax | It Indicates the Maximum value of the slider. |
| aria-orientation | It Indicates the Slider Orientation. |
| aria-label | Slider left and right button label text (increment and decrement). |
| aria-labelledby | It indicates the name of the Slider. |

## Keyboard interaction

The Keyboard interaction of the Slider component is designed based on the
[WAI-ARIA Practices](https://www.w3.org/TR/wai-aria-practices/#slider ) described for Slider.
Users can use the following shortcut keys to interact with the Slider.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
<b>Keyboard shortcuts</b></td><td>
<b>Actions</b></td></tr>
<tr>
<td>
<kbd>Right Arrow</kbd>&nbsp;&nbsp; &#124;&nbsp;&nbsp; <kbd>Up Arrow</kbd></td><td>
Increase the Slider value.
</td></tr>
<tr>
<td>
<kbd>Left Arrow</kbd>&nbsp;&nbsp; &#124;&nbsp;&nbsp; <kbd>Down Arrow</kbd></td><td>
Decrease the Slider value.</td></tr>
<tr>
<td>
<kbd>Home</kbd></td><td>
Moves to the start value (for Range Slider when the second thumb is focused and the Home key is pressed, it moves to the first thumb value).</td></tr>
<tr>
<td>
<kbd>End</kbd></td><td>
Moves to the end value (for Range Slider when the first thumb is focused and the End key is pressed, it moves to the second thumb value).</td></tr>
<tr>
<td>
<kbd>Page Up</kbd></td><td>
Increases the Slider by `largeStep` value.</td></tr>
<tr>
<td>
<kbd>Page Down</kbd></td><td>
Decreases the Slider by `largeStep` value.</td></tr>
</table>

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public ticks01: TicksDataModel = {
    placement: "After",
    largeStep: 20,
    smallStep: 10,
    showSmallTicks: true
  };
  public tooltip01: TooltipDataModel = { placement: "Before", isVisible: true, showOn: "Always" };

  public ticks02: TicksDataModel = { placement: "After", largeStep: 1 };
  public tooltip02: TooltipDataModel = { placement: "Before", isVisible: true };

  public value = 30;
  public step = 10;
  public showButtons = true;

  renderingTicksHandler(args: SliderTickEventArgs) {
    // Weekdays Array
    let daysArr: string[] = [
      "Sunday",
      "Monday",
      "Tuesday",
      "Wednesday",
      "Thrusday",
      "Friday",
      "Saturday"
    ];
    // Customizing each ticks text into weeksdays
    args.text = daysArr[parseFloat(args.value.toString())];
  }

  tooltipChangeHandler(args: SliderTooltipEventArgs) {
    // Customizing tooltip to display the Day (in numeric) of the week
    args.text = "Day " + (Number(args.value) + 1).toString();
  }

  render() {
    return (
      <div id="container">
        <div className="wrap">
          <div className="label">Slider without formatted values</div>
          <SliderComponent
            id="slider"
            step={this.step}
            value={this.value}
            tooltip={this.tooltip01}
            ticks={this.ticks01}
            type="MinRange"
            showButtons={true}
          />
        </div>
        <div className="wrap">
          <div className="label">Slider with formatted values</div>
          <SliderComponent
            id="slider1"
            min={0}
            max={6}
            step={1}
            value={2}
            tooltip={this.tooltip02}
            ticks={this.ticks02}
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
