---
title: "Slider Formatting"
component: "Slider"
description: "React slider supports formatting to customize slider values like time, currency & km, values, also displayed in ticks & tooltip."
---

# Formatting

The `format` feature used to customize the units of Slider values to desired format. The formatted values will also be applied to
the ARIA attributes of the slider. There are two ways of achieving formatting in slider.

* Use the `format` API of slider which utilizes our `Internationalization` to format values.

* Customize using the events namely `renderingTicks` and `tooltipChange`.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public tooltip = { isVisible: true, format: "C2" };
  public value = 30;
  // Slider ticks customization
  public ticks: TicksDataModel = {
    placement: "After",
    format: "C2",
    largeStep: 20,
    smallStep: 10,
    showSmallTicks: true
  };
  render() {
    return (
      <div id="container">
        <div className="wrap">
          <SliderComponent
            id="slider"
            min={0}
            max={100}
            value={this.value}
            tooltip={this.tooltip}
            ticks={this.ticks}
          />
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Using format API

In this method, we have different predefined formatting styles like Numeric (N), Percentage (P), Currency (C) and `#` specifiers. In this
below example we have formatted the `ticks` and `tooltip` values into percentage.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public tooltip: TooltipDataModel = {
    placement: "Before",
    isVisible: true,
    showOn: "Always",
    format: "P0"
  };
  public value = 0.3;
  // Slider ticks customization
  public ticks: TicksDataModel = {
    placement: "After",
    largeStep: 0.2,
    smallStep: 0.1,
    showSmallTicks: true,
    format: "P0"
  };
  render() {
    return (
      <div id="container">
        <div className="wrap">
          <SliderComponent
            id="slider"
            min={0}
            max={1}
            step={0.01}
            value={this.value}
            tooltip={this.tooltip}
            ticks={this.ticks}
          />
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Using Events

In this method, we will be retrieving the values from the slider events then process them to desired formatted the values.
In this sample we have customized the `ticks` values into weekdays as one formatting and `tooltip` values into day of the week as another formatting.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true };
  public value = 2;
  // Slider ticks customization
  public ticks: TicksDataModel = { placement: "After", largeStep: 1 };

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
          <SliderComponent
            id="slider"
            min={0}
            max={6}
            step={1}
            value={this.value}
            tooltip={this.tooltip}
            ticks={this.ticks}
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
