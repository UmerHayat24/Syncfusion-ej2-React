# Customize slider thumb

Slider appearance can be customized through CSS. By overriding the slider CSS classes, you can customize the thumb. By default, slider has unique class `e-handle` for slider thumb. You can override the following class as per your requirement.

```css
.e-control.e-slider .e-handle {
    background-image: url('https://ej2.syncfusion.com/demos/src/slider/images/thumb.png');
    background-color: transparent;
    height: 25px;
    width: 25px;
}
#square_slider.e-control.e-slider .e-handle {
    border-radius: 0%;
    background-color: #f9920b;
    border: 0;
}
#circle_slider.e-control.e-slider .e-handle {
    border-radius: 50%;
    background-color: #f9920b;
    border: 0;
}
#oval_slider.e-control.e-slider .e-handle {
    height: 25px;
    width: 8px;
    top: 3px;
    border-radius: 15px;
    background-color: #f9920b;
}
```

Here, in the sample, the slider thumb has been customized to square, circle, oval shapes, and background image has also been customized.

{% tab template="slider/thumb-custom", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent, SliderTickRenderedEventArgs, SliderTickEventArgs } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  render() {
    return (
      <div id='container'>
        <div className="col-lg-12 control-section">
          <div className="slider-content-wrapper">
            <div className="slider_container">
                <div className="labelText slider-userselect">Square</div>
                <SliderComponent id='square_slider' min={0} max={100} value={30} />
            </div>

            <div className="slider_container">
                <div className="labelText slider-userselect">Circle</div>
                <SliderComponent id='circle_slider' min={0} max={100} value={30} />
            </div>

            <div className="slider_container">
                <div className="labelText slider-userselect">Oval</div>
                <SliderComponent id='oval_slider' min={0} max={100} value={30} />
            </div>

            <div className="slider_container">
                <div className="labelText slider-userselect">Custom image</div>
                <SliderComponent id='image_slider' min={0} max={100} value={30} />
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
