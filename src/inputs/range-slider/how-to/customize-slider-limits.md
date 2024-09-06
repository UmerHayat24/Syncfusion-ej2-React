# Customize slider limits

Slider appearance can be customized via CSS. By overriding the slider CSS classes, the slider limit bar can be customized.

```css
.e-slider-container.e-horizontal .e-limits {
  background-color: rgba(69, 100, 233, 0.46);
}
```

Here, the limit bar is customized with different background color. By default, the slider has class `e-limits` for limits bar.
You can override the class with our own color values as given in the following code snippet.

{% tab template="slider/limits-custom", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent, SliderChangeEventArgs } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  private defaultObj: SliderComponent;
  private value: number[] = [30, 70];

  private ticks: object = { placement: 'Before', largeStep: 20, smallStep: 5, showSmallTicks: true };
  // Initialize tooltip with placement and showOn
  private tooltip: object = { isVisible: true, placement: 'Before', showOn: 'Focus' };

  // Set the limit values for the minrange slider
  private minLimits: object = { enabled: true, minStart: 10, minEnd: 40 };
  // Set the limit values for the range slider
  private rangeLimits: object = { enabled: true, minStart: 10, minEnd: 40, maxStart: 60, maxEnd: 90 };

  render() {
    return (
      <div id='container'>
      <div className="content-wrapper">
        <div className='sliderwrap'>
            <label className="userselect">MinRange Slider With Limits</label>
            <SliderComponent id='minrange'
              type='MinRange'
                min={0} max={100} value={30} ticks={this.ticks} tooltip={this.tooltip} limits={this.minLimits} />
        </div>

        <div className='sliderwrap'>
            <label className="userselect">Range Slider With Limits</label>
            <SliderComponent id='range' type='Range'
                min={0} max={100} value={this.value} ticks={this.ticks} tooltip={this.tooltip} limits={this.rangeLimits} />
        </div>
      </div>
    </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
