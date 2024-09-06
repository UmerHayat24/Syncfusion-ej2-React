---
title: "Slider Ticks"
component: "Slider"
description: "React slider visually represents the slider values with small and large ticks placed before, after, or both, of the slider bar."
---

# Ticks

The Ticks in Slider supports you to easily identify the current value/values of the Slider. It contains
`smallStep` and `largeStep`. The value of the major ticks alone
will be displayed in the slider. In order to enable/disable the small ticks, use the `showSmallTicks` property.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true, showOn: "Always" };
  public value = 30;
  // Slider ticks customization
  public ticks: TicksDataModel = {
    placement: "After",
    largeStep: 20,
    smallStep: 10,
    showSmallTicks: true
  };
  render() {
    return (
      <div id="container">
        <div className="wrap">
          <SliderComponent id="slider" value={this.value} tooltip={this.tooltip} ticks={this.ticks} />
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Step

When the Slider is moved, it increases/decreases the value
based on the step value. By default, the value is increased/decreased by 1. Use the `step` property to change the increment step value.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public ticks: TicksDataModel = {
    placement: "After",
    largeStep: 20,
    smallStep: 10,
    showSmallTicks: true
  };
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true, showOn: "Always" };
  public value = 30;
  // Enables step
  public step = 10;

  render() {
    return (
      <div id="container">
        <div className="wrap">
          <SliderComponent
            id="slider"
            value={this.value}
            step={this.step}
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

## Min and Max

Enables the minimum/starting and maximum/ending value of the Slider, by using the `min` and `max`
property. By default, the minimum value is 1 and maximum value is 100. In the following sample the slider is
rendered with the min value as 100 and max value as 1000.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public ticks: TicksDataModel = {
    placement: "After",
    largeStep: 200,
    smallStep: 100,
    showSmallTicks: true
  };
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true, showOn: "Always" };
  // Minimum value
  public min = 100;
  // Maximum value
  public max = 1100;
  // Slider current value
  public value = 400;

  render() {
    return (
      <div id="container">
        <div className="wrap">
          <SliderComponent
            id="slider"
            min={this.min}
            max={this.max}
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
