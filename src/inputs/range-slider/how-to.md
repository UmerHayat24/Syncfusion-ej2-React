---
title: "Slider How To"
component: "Slider"
description: "React Slider how to section, date format slider, time format slider, slider validation, slider limits and customization of slider bar, thumb & ticks."
---

# How To

## Value formatting using slider

### Date Format

The Date formatting can be achieved in `ticks` and `tooltip` using `renderingTicks` and `tooltipChange` events respectively. The process
of formatting is explained in the below sample.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  private defaultObj: SliderComponent;

  public min = new Date("2013-06-13").getTime();
  public max = new Date("2013-06-21").getTime();
  public step = 86400000;
  public value = new Date("2013-06-15").getTime();

  // Slider ticks customization
  public ticks= { placement: 'After', largeStep: 2 * 86400000 };
  public tooltip= { placement: 'Before', isVisible: true };

  renderingTicksHandler (args: SliderTickEventArgs) {
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
        <div id='container'>
          <div className='wrap'>
            <SliderComponent id='slider' min={this.min} max={this.max} value={this.value} step={this.step}
            tooltip={this.tooltip} ticks={this.ticks} showButtons={true} ref={(slider) => { this.defaultObj = slider }}
            tooltipChange={this.tooltipChangeHandler.bind(this)} renderingTicks={this.renderingTicksHandler.bind(this)} />
          </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

### Time Format

The time formatting can be achieved same as the date formatting using `renderingTicks` and `change` events. The process of time formatting is
explained in the below sample.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  private defaultObj: SliderComponent;

  public min = new Date(2013, 6, 13, 11).getTime();
  public max = new Date(2013, 6, 13, 17).getTime();
  public value = new Date(2013, 6, 13, 13).getTime();
  public step = 3600000;

  // Slider ticks customization
  public ticks= { placement: 'After', largeStep: 2 * 3600000 };
  public tooltip= { placement: 'Before', isVisible: true };

  renderingTicksHandler (args: SliderTickEventArgs) {
    let totalMiliSeconds = Number(args.value);
    let custom = { hour: '2-digit', minute: '2-digit' };
    args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
  }

  tooltipChangeHandler(args: SliderTooltipEventArgs) {
    let totalMiliSeconds = Number(args.text);
    let custom = { hour: '2-digit', minute: '2-digit' };
    args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
  }

  render() {
    return (
        <div id='container'>
          <div className='wrap'>
            <SliderComponent id='slider' min={this.min} max={this.max} value={this.value} step={this.step} tooltip={this.tooltip}
            ticks={this.ticks} showButtons={true} ref={(slider) => { this.defaultObj = slider }}
            tooltipChange={this.tooltipChangeHandler.bind(this)} renderingTicks={this.renderingTicksHandler.bind(this)} />
          </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

### Numeric Value Customization

The numeric values can be formatted into different decimal digits or fixed number of whole numbers or to represent the units. The Numeric
processing is demonstrated below.

{% tab template="slider/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {

  private defaultObj: SliderComponent;

  // Slider ticks customization
  public ticks01 = { placement: 'After', format: '##.## Km', largeStep: 20, smallStep: 10, showSmallTicks: true };
  public tooltip01 = { isVisible: true, format: '##.## Km' };

  public ticks02 = { placement: 'After', format: '##.#00', largeStep: 0.02, smallStep: 0.01, showSmallTicks: true };
  public tooltip02 = { isVisible: true, format: '##.#00' };

  public tooltip03 = { isVisible: true, format: '00##' };
  public ticks03 = { placement: 'After', format: '00##', largeStep: 20, smallStep: 10, showSmallTicks: true };

  render() {
    return (
      <div id='container'>

        <div className='wrap'>
            <div className='label'>Slider formatted with unit representation</div>
            <SliderComponent id='slider' min={0} max={100} value={30} step={1} tooltip={this.tooltip01} ticks={this.ticks01} />
        </div>

        <div className='wrap'>
            <div className='label'>Slider formatted with three decimal specifiers</div>
            <SliderComponent id='slider1' min={0.1} max={0.2} value={0.13} step={0.01} tooltip={this.tooltip02} ticks={this.ticks02} />
        </div>

        <div className='wrap'>
            <div className='label'>Slider formatted with two leading zeros</div>
            <SliderComponent id='slider2' min={0} max={100} value={30} step={1} tooltip={this.tooltip03} ticks={this.ticks03} />
        </div>
    </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

### Customize the bar

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

  private defaultObj: SliderComponent;
  private sliderTrack: HTMLElement;
  private sliderHandle: HTMLElement;

  private changeEvent (args: SliderChangeEventArgs): void {
    if (args.value > 0 && args.value <= 25) {
        // Change handle and range bar color to green when
        (this.sliderHandle as HTMLElement).style.backgroundColor = 'green';
        (this.sliderTrack as HTMLElement).style.backgroundColor = 'green';
    } else if (args.value > 25 && args.value <= 50) {
        // Change handle and range bar color to royal blue
        (this.sliderHandle as HTMLElement).style.backgroundColor = 'royalblue';
        (this.sliderTrack as HTMLElement).style.backgroundColor = 'royalblue';
    } else if (args.value > 50 && args.value <= 75) {
        // Change handle and range bar color to dark orange
        (this.sliderHandle as HTMLElement).style.backgroundColor = 'darkorange';
        (this.sliderTrack as HTMLElement).style.backgroundColor = 'darkorange';
    } else if (args.value > 75 && args.value <= 100) {
        // Change handle and range bar color to red
        (this.sliderHandle as HTMLElement).style.backgroundColor = 'red';
        (this.sliderTrack as HTMLElement).style.backgroundColor = 'red';
    }
  }

  private created(): void {
    this.sliderTrack = document.getElementById('dynamic_color_slider').querySelector('.e-range');
    this.sliderHandle = document.getElementById('dynamic_color_slider').querySelector('.e-handle');
    (this.sliderHandle as HTMLElement).style.backgroundColor = 'green';
    (this.sliderTrack as HTMLElement).style.backgroundColor = 'green';
  }

  render() {
    return (
      <div id='container'>
        <div className="col-lg-12 control-section">
          <div className="slider-content-wrapper">
              <div className="slider_container">
                <div className="slider-labeltext slider_userselect">Height</div>
                <SliderComponent id='height_slider' min={0} max={100} value={30} />
              </div>

              <div className="slider_container">
                  <div className="slider-labeltext slider_userselect">Gradient color</div>
                  <SliderComponent id='gradient_slider' type='MinRange' min={0} max={100} value={30} />
              </div>

              <div className="slider_container">
                  <div className="slider-labeltext slider_userselect">Dynamic thumb and selection bar color</div>
                  <SliderComponent id='dynamic_color_slider' ref={(slider) => { this.defaultObj = slider }}
                type='MinRange' min={0} max={100} value={30} change={this.changeEvent.bind(this)}
                  created={this.created.bind(this)} />
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

## Customize the limits

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

## Customize the ticks

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

  private defaultObj: SliderComponent;
  private value: number[] = [30, 70];

  private icon: object = { placement: 'Before', largeStep: 20 };

  private custom: object = { placement: 'Both', largeStep: 20, smallStep: 5 };


  private iconTicks(args: SliderTickEventArgs): void {
    if (args.tickElement.classList.contains('e-large')) {
        args.tickElement.classList.add('e-custom');
    }
  }

  private customTicks(args: SliderTickRenderedEventArgs): void {
    let li: any = args.ticksWrapper.getElementsByClassName('e-large');
    let remarks: any = ['Very Poor', 'Poor', 'Average', 'Good', 'Very Good', 'Excellent'];
    for (let i: number = 0; i < li.length; ++i) {
        (li[i].querySelectorAll('.e-tick-both')[1] as HTMLElement).innerText = remarks[i];
    }
  }

  render() {
    return (
      <div id='container'>
        <div className="col-lg-12 control-section">
          <div className="slider-content-wrapper">
              <div className="slider_container" id="slider_wrapper">
                <div className="slider_labelText userselect">Dynamic ticks color</div>
                <SliderComponent id='ticks_slider'
                  type='MinRange'
                  min={0} max={100} step={5} value={30} ticks={this.icon} renderingTicks={this.iconTicks.bind(this)} />
              </div>

              <div className="slider_container">
                <div className="slider_labelText userselect">Ticks with legends</div>
                <SliderComponent id='slider' type='MinRange'
                  min={0} max={100} value={this.value} ticks={this.custom} renderedTicks={this.customTicks.bind(this)} />
              </div>
            <div/>
          </div>
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Customize the thumb

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

## Validate the slider using FormValidator

The Slider component can be validated using our [FormValidator](https://ej2.syncfusion.com/documentation/form-validator/?lang=typescript). The following steps walk-through slider validation.

* Render slider component inside a form.
* Bind [changed](https://ej2.syncfusion.com/react/documentation/slider/api-sliderComponent.html#changed) event in the slider
component to validate the slider value when the value changes.
* Initialize and render FormValidator for the form using form ID.

```typescript

// Initialize Form validation
let formObj: FormValidator;
formObj = new FormValidator("#formId", options);

```

* Set the required property in the FormValidator [rules](https://ej2.syncfusion.com/documentation/form-validator/api-formValidator.html?lang=typescript#rules) collection. Here, the [min](https://ej2.syncfusion.com/react/documentation/slider/api-sliderComponent.html#min) property of slider that sets the minimum value in the slider component is set, and it has hidden input as enable `validateHidden` property is set to true.

```typescript

// Slider element
<div id="default" name="slider"></div>

// sets required property in the FormValidator rules collection
let options: FormValidatorModel = {
  rules: {
    'default': {
      validateHidden: true,
      min: [6, "You must select value greater than 5"]
    }
  }
};

```

> Form validation is done either by ID or name value of the slider component. Above ID of the slider is used to validate it.

Using slider name: Render slider with name attribute. In the following code snippet, name attribute value of slider is used for
form validation.

```typescript

// Slider element
<div id="default" name="slider"></div>

// sets required property in the FormValidator rules collection
let options: FormValidatorModel = {
  rules: {
    'slider': {
      validateHidden: true,
      min: [6, "You must select value greater than 5"]
    }
  }
};

```

* Validate the form using [validate](https://ej2.syncfusion.com/documentation/form-validator/api-formValidator.html?lang=typescript#validate) method, and it validates the slider value with the defined rules collection and returns the result. If user selects the value less than the minimum value, form will not submit.

```typescript

formObj.validate();

```

* Slider validation can be done during value changes in slider. Refer to the following code snippet.

```typescript

// change event handler for slider
function onChanged(args: any) {
  formObj.validate();
}

```

The `FormValidator` has following default validation rules, which are used to validate the Slider component.

| Rules | Description | Example |
| ------------- | ------------- | ------------- |
| `max` | Slider component must have value less than or equal to `max` number | if `max: 3`, **3** is valid and **4** is invalid |
| `min` | Slider component must have value greater than or equal to `min` number | if `min: 4`, **5** is valid and **2** is invalid |
| `regex` | Slider component must have valid value in `regex` format | if `regex: '/4/`, **4** is valid and **1** is invalid |
| `range` | Slider component must have value between `range` number | if `range: [4,5]`, **4** is valid and **6** is invalid |

{% tab template="slider/form-validation", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

export default class App extends React.Component<{}, {}> {
  private ticks: object = { placement: 'Before', largeStep: 20, smallStep: 5, showSmallTicks: true };
  private value: number[] = [30, 70];

  // sets required property in the FormValidator rules collection
  private minOptions: FormValidatorModel = {
    rules: {
      'min-slider': {
        validateHidden: true,
        min: [40, "You must select value greater than or equal to 40"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private maxOptions: FormValidatorModel = {
    rules: {
      'max-slider': {
        validateHidden: true,
        max: [40, "You must select value less than or equal to 40"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private valOptions: FormValidatorModel = {
    rules: {
      'val-slider': {
        validateHidden: true,
        regex: [/40/, "You must select value equal to 40"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private rangeOptions: FormValidatorModel = {
    rules: {
      'range-slider': {
        validateHidden: true,
        range: [40, 80, "You must select values between 40 and 80"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private customOptions: FormValidatorModel = {
    rules: {
      'custom-slider': {
        validateHidden: true,
        range: [this.validateRange.bind(this), "You must select values between 40 and 80"]
      }
    }
  };

  // Initialize Form validation
  private formMinObj: FormValidator;

  private formMaxObj: FormValidator;

  private formValObj: FormValidator;

  private formRangeObj: FormValidator;

  private formCustomObj: FormValidator;

  public componentDidMount(): void {
    this.formMinObj = new FormValidator("#formMinId", this.minOptions);
    this.formMaxObj = new FormValidator("#formMaxId", this.maxOptions);
    this.formValObj = new FormValidator("#formValId", this.valOptions);
    this.formRangeObj = new FormValidator("#formRangeId", this.rangeOptions);
    this.formCustomObj = new FormValidator("#formCustomId", this.customOptions);
  }

  private onMinChanged(args: any): void {
    // validate the slider value in the form
    this.formMinObj.validate();
  }

  private onMaxChanged(args: any): void {
    // validate the slider value in the form
    this.formMaxObj.validate();
  }

  private onValChanged(args: any): void {
    // validate the slider value in the form
    this.formValObj.validate();
  }

  private onRangeChanged(args: any) {
    // validate the slider value in the form
    this.formRangeObj.validate();
  }

  private onCustomChanged(args: any) {
    // validate the slider value in the form
    this.formCustomObj.validate();
  }

  private SliderCustomObj: SliderComponent;

  private validateRange(args: any) {
    return (this.SliderCustomObj.value as number[])[0] >= 40 && (this.SliderCustomObj.value as number[])[1] <= 80;
  }

  render() {
    return (
      <div id='container'>
        <div className="col-lg-12 control-section">
          <div className="content-wrapper">
              <div className="form-title">
                  <span>Min</span>
              </div>
              <form id="formMinId" className="form-horizontal">
                  <div className="form-group">
                      <div className="e-float-input">
                          <SliderComponent id='min-slider' name="min-slider" type='MinRange' value={30} ticks={this.ticks}
                            changed={this.onMinChanged.bind(this)} />
                      </div>
                  </div>
              </form>
              <div className="form-title">
                  <span>Max</span>
              </div>
              <form id="formMaxId" className="form-horizontal">
                  <div className="form-group">
                      <div className="e-float-input">
                          <SliderComponent id='max-slider' name="max-slider" type='MinRange' value={30} ticks={this.ticks}
                            changed={this.onMaxChanged.bind(this)} />
                      </div>
                  </div>
              </form>
              <div className="form-title">
                  <span>Value</span>
              </div>
              <form id="formValId" className="form-horizontal">
                  <div className="form-group">
                      <div className="e-float-input">
                          <SliderComponent id='val-slider' name='val-slider' type='MinRange' value={30} ticks={this.ticks}
                            changed={this.onValChanged.bind(this)} />
                      </div>
                  </div>
              </form>
              <div className="form-title">
                  <span>Range</span>
              </div>
              <form id="formRangeId" className="form-horizontal">
                  <div className="form-group">
                      <div className="e-float-input">
                          <SliderComponent id='range-slider' name='range-slider' type='MinRange' value={30} ticks={this.ticks}
                            changed={this.onRangeChanged.bind(this)} />
                      </div>
                  </div>
              </form>
              <div className="form-title">
                  <span>Custom</span>
              </div>
              <form id="formCustomId" className="form-horizontal">
                  <div className="form-group">
                      <div className="e-float-input">
                          <SliderComponent id='custom-slider' name='custom-slider' type='Range' value={this.value}
                            ticks={this.ticks} changed={this.onCustomChanged.bind(this)}
                            ref={(slider) => { this.SliderCustomObj = slider }} />
                      </div>
                  </div>
              </form>
          </div>
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
