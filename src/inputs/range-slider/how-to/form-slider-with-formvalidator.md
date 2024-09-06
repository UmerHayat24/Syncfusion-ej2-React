# Form slider with Form Validator

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
  private ticks: object = { placement: "Before", largeStep: 20, smallStep: 5, showSmallTicks: true };
  private value: number[] = [30, 70];

  // sets required property in the FormValidator rules collection
  private minOptions: FormValidatorModel = {
    rules: {
      "min-slider": {
        validateHidden: true,
        min: [40, "You must select value greater than or equal to 40"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private maxOptions: FormValidatorModel = {
    rules: {
      "max-slider": {
        validateHidden: true,
        max: [40, "You must select value less than or equal to 40"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private valOptions: FormValidatorModel = {
    rules: {
      "val-slider": {
        validateHidden: true,
        regex: [/40/, "You must select value equal to 40"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private rangeOptions: FormValidatorModel = {
    rules: {
      "range-slider": {
        validateHidden: true,
        range: [40, 80, "You must select values between 40 and 80"]
      }
    }
  };

  // sets required property in the FormValidator rules collection
  private customOptions: FormValidatorModel = {
    rules: {
      "custom-slider": {
        validateHidden: true,
        range: [this.validateRange.bind(this), "You must select values between 40 and 80"]
      }
    }
  };

  // Initialize Form validation
  private formMinObj: FormValidator = null as any;

  private formMaxObj: FormValidator = null as any;

  private formValObj: FormValidator = null as any;

  private formRangeObj: FormValidator = null as any;

  private formCustomObj: FormValidator = null as any;

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

  private SliderCustomObj: SliderComponent = null as any;

  private validateRange(args: any) {
    return (
      (this.SliderCustomObj.value as number[])[0] >= 40 &&
      (this.SliderCustomObj.value as number[])[1] <= 80
    );
  }

  render() {
    return (
      <div id="container">
        <div className="col-lg-12 control-section">
          <div className="content-wrapper">
            <div className="form-title">
              <span>Min</span>
            </div>
            <form id="formMinId" className="form-horizontal">
              <div className="form-group">
                <div className="e-float-input">
                  <SliderComponent
                    id="min-slider"
                    name="min-slider"
                    type="MinRange"
                    value={30}
                    ticks={this.ticks}
                    changed={this.onMinChanged.bind(this)}
                  />
                </div>
              </div>
            </form>
            <div className="form-title">
              <span>Max</span>
            </div>
            <form id="formMaxId" className="form-horizontal">
              <div className="form-group">
                <div className="e-float-input">
                  <SliderComponent
                    id="max-slider"
                    name="max-slider"
                    type="MinRange"
                    value={30}
                    ticks={this.ticks}
                    changed={this.onMaxChanged.bind(this)}
                  />
                </div>
              </div>
            </form>
            <div className="form-title">
              <span>Value</span>
            </div>
            <form id="formValId" className="form-horizontal">
              <div className="form-group">
                <div className="e-float-input">
                  <SliderComponent
                    id="val-slider"
                    name="val-slider"
                    type="MinRange"
                    value={30}
                    ticks={this.ticks}
                    changed={this.onValChanged.bind(this)}
                  />
                </div>
              </div>
            </form>
            <div className="form-title">
              <span>Range</span>
            </div>
            <form id="formRangeId" className="form-horizontal">
              <div className="form-group">
                <div className="e-float-input">
                  <SliderComponent
                    id="range-slider"
                    name="range-slider"
                    type="MinRange"
                    value={30}
                    ticks={this.ticks}
                    changed={this.onRangeChanged.bind(this)}
                  />
                </div>
              </div>
            </form>
            <div className="form-title">
              <span>Custom</span>
            </div>
            <form id="formCustomId" className="form-horizontal">
              <div className="form-group">
                <div className="e-float-input">
                  <SliderComponent
                    id="custom-slider"
                    name="custom-slider"
                    type="Range"
                    value={this.value}
                    ticks={this.ticks}
                    changed={this.onCustomChanged.bind(this)}
                    ref={slider => {
                      this.SliderCustomObj = slider as any;
                    }}
                  />
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
