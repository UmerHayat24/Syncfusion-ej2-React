# Customize slider bar

Slider appearance can be customized through CSS. By overriding the slider CSS classes, you can customize the slider bar.
The slider bar can be customized with different themes. By default, slider have class name e-slider-track for bar. The
class can be overridden with our own color values like the following code snippet.

```css
.e-control.e-slider .e-slider-track .e-range {
  background: linear-gradient(left, #e1451d 0, #fdff47 17%, #86f9fe 50%, #2900f8 65%, #6e00f8 74%, #e33df9 83%, #e14423 100%);
}
```

```typescript
private change(args: SliderChangeEventArgs) {
  if (args.value > 0 && args.value <= 25) {
      // Change handle and range bar color to green when
      (sliderHandle as HTMLElement).style.backgroundColor = 'green';
      (sliderTrack as HTMLElement).style.backgroundColor = 'green';
  } else if (args.value > 25 && args.value <= 50) {
      // Change handle and range bar color to royal blue
      (sliderHandle as HTMLElement).style.backgroundColor = 'royalblue';
      (sliderTrack as HTMLElement).style.backgroundColor = 'royalblue';
  } else if (args.value > 50 && args.value <= 75) {
      // Change handle and range bar color to dark orange
      (sliderHandle as HTMLElement).style.backgroundColor = 'darkorange';
      (sliderTrack as HTMLElement).style.backgroundColor = 'darkorange';
  } else if (args.value > 75 && args.value <= 100) {
      // Change handle and range bar color to red
      (sliderHandle as HTMLElement).style.backgroundColor = 'red';
      (sliderTrack as HTMLElement).style.backgroundColor = 'red';
  }
}
```

You can also apply background color for a certain range depending upon slider values, using change event.

{% tab template="slider/bar", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent, SliderChangeEventArgs } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  private defaultObj: SliderComponent = null as any;
  private sliderTrack: HTMLElement = null as any;
  private sliderHandle: HTMLElement = null as any;

  private changeEvent(args: SliderChangeEventArgs): void {
    if (args.value > 0 && args.value <= 25) {
      // Change handle and range bar color to green when
      this.sliderHandle.style.backgroundColor = "green";
      this.sliderTrack.style.backgroundColor = "green";
    } else if (args.value > 25 && args.value <= 50) {
      // Change handle and range bar color to royal blue
      this.sliderHandle.style.backgroundColor = "royalblue";
      this.sliderTrack.style.backgroundColor = "royalblue";
    } else if (args.value > 50 && args.value <= 75) {
      // Change handle and range bar color to dark orange
      this.sliderHandle.style.backgroundColor = "darkorange";
      this.sliderTrack.style.backgroundColor = "darkorange";
    } else if (args.value > 75 && args.value <= 100) {
      // Change handle and range bar color to red
      this.sliderHandle.style.backgroundColor = "red";
      this.sliderTrack.style.backgroundColor = "red";
    }
  }

  private created(): void {
    this.sliderTrack = this.defaultObj.element.querySelector(".e-range") as any;
    this.sliderHandle = this.defaultObj.element.querySelector(".e-handle") as any;
    this.sliderHandle.style.backgroundColor = "green";
    this.sliderTrack.style.backgroundColor = "green";
  }

  render() {
    return (
      <div id="container">
        <div className="col-lg-12 control-section">
          <div className="slider-content-wrapper">
            <div className="slider_container">
              <div className="slider-labeltext slider_userselect">Height</div>
              <SliderComponent id="height_slider" min={0} max={100} value={30} />
            </div>

            <div className="slider_container">
              <div className="slider-labeltext slider_userselect">Gradient color</div>
              <SliderComponent id="gradient_slider" type="MinRange" min={0} max={100} value={30} />
            </div>

            <div className="slider_container">
              <div className="slider-labeltext slider_userselect">
                Dynamic thumb and selection bar color
              </div>
              <SliderComponent
                id="dynamic_color_slider"
                ref={slider => {
                  this.defaultObj = slider as any;
                }}
                type="MinRange"
                min={0}
                max={100}
                value={30}
                change={this.changeEvent.bind(this) as any}
                created={this.created.bind(this)}
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
