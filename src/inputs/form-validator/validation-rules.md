# Validation Rules

## Default Rules

The `FormValidator` has following default validation rules, which are used to validate the form.

| Rules | Description | Example |
| ------------- | ------------- | ------------- |
| `required` | The form input element must have any input values | a or 1 or - |
| `email` | The form input element must have valid `email` format values | `form@syncfusion.com` |
| `url` | The form input element must have valid `url` format values | `http://syncfusion.com/` |
| `date` | The form input element must have valid `date` format values | 05/15/2017 |
| `dateIso` | The form input element must have valid `dateISO` format values | 2017-05-15 |
| `number` | The form input element must have valid `number` format values | 1.0 or 1 |
| `digit` | The form input element must have valid `digit` values | 1 |
| `maxLength` | Input value must have less than or equal to `maxLength` character length | if `maxLength: 5`, **check** is valid and **checking** is invalid |
| `minLength` | Input value must have greater than or equal to `minLength` character length | if `minLength: 5`, **testing** is valid and **test** is invalid |
| `rangeLength` | Input value must have value between `rangeLength` character length | if `rangeLength: [4,5]`, **test** is valid and **key** is invalid |
| `range` | Input value must have value between `range` number | if `range: [4,5]`, **4** is valid and **6** is invalid |
| `max` | Input value must have less than or equal to `max` number | if `max: 3`, **3** is valid and **4** is invalid |
| `min` | Input value must have greater than or equal to `min` number | if `min: 4`, **5** is valid and **2** is invalid |
| `regex` | Input value must have valid `regex` format | if `regex: '^[A-z]+$'`, **a** is valid and **1** is invalid |

> The [`rules`](https://ej2.syncfusion.com/documentation/api/form-validator/#rules) option should map the input element's `name` attribute.
> The `FormValidator` library only validates the mapped input elements.

## Defining Custom Rules

You can also define custom rules in the [`rules`](https://ej2.syncfusion.com/documentation/api/form-validator/#rules) property and validate the form with custom logics.

The custom validation method need to return the boolean value for validating an input.

{% tab template="form-validator/validation", sourceFiles="app/**/*.tsx"   %}

```typescript
import { select } from '@syncfusion/ej2-base';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class Validation extends React.Component<{}, {}> {
public dialogInstance: DialogComponent;
public formObject: FormValidator;
private animationSettings: object = { effect: 'Zoom' };
public floatFocus(args: any): void {
  args.target.parentElement.classList.add('e-input-focus');
}
public floatBlur(args: any): void {
  args.target.parentElement.classList.remove('e-input-focus');
}
  // Dialog will be closed, while clicking on overlay
  public onOverlayClick() {
        this.dialogInstance.hide();
  }
  public componentDidMount(): void {
        const options: FormValidatorModel = {
          // add the rules for validation
         rules: {
          'email': {
            required: [true, '* Enter your email']
          },
          'mobile': {
            required: [true, '* Enter your mobile number']
          },
          'name': {
              required: [true, '* Enter your name']
          },
        }
      };
      // initialize the form validator
      this.formObject = new FormValidator('#form1', options);
  }

  public onSubmitClick(): void {
  if(this.formObject.validate()) {
    this.formObject.element.reset();
    this.dialogInstance.show();
      }
  }

public render(): JSX.Element {
  return (    <div className = 'control-pane'>
    <div className='control-section col-lg-12'>
      <h4 className="form-title">Validation Support</h4>
      <div className='validation_wrapper'>
        <div className="control_wrapper" id="control_wrapper">
          <form id="form1"  method="post">
            <div className="form-group" >
              <div className="e-float-input">
                <input type="text" id="name" name="name" onFocus= {this.floatFocus} onBlur= {this.floatBlur}  data-msg-containerid="nameError" />
                <span className="e-float-line"/>
                <label className="e-float-text e-label-top" htmlFor="name">Name</label>
              </div>
              <div id="nameError"/>
            </div>
            <div className="form-group">
              <div className="e-float-input">
                <input type="email" id="Email" name="email" data-msg-containerid="mailError"/>
                <span className="e-float-line"/>
                <label className="e-float-text e-label-top" htmlFor="email" >Email</label>
              </div>
              <div id="mailError"/>
            </div>
            <div className="form-group" >
              <div className="e-float-input">
                <input type="text" id="mobileno" name="mobile" data-msg-containerid="noError" />
                <span className="e-float-line"/>
                <label className="e-float-text e-label-top"  htmlFor="mobile" >Mobile no</label>
              </div>
              <div id="noError"/>
            </div>
          </form>
          <br/>
          <br/>
          <div className="submitBtn">
            <button className="submit-btn e-btn" onClick={this.onSubmitClick = this.onSubmitClick.bind(this)} id="submit-btn">Submit</button>
          </div>
          <div id="confirmationDialog"/> </div>
        </div>
      </div>
      <DialogComponent id="defaultdialog" isModal={true} visible ={false} content = 'Your details has been updated successfully, Thank you' animationSettings={this.animationSettings} width={'50%'}  ref={dialog => this.dialogInstance = dialog!}
      target={'.control-section'} overlayClick={this.onOverlayClick=this.onOverlayClick.bind(this)} />
    </div>) }
}

ReactDOM.render(<Validation />, document.getElementById('validation'));
```

{% endtab %}

## Adding or Removing Rules

After creating `FormValidator` object, you can add
more rules to an input element by using [`addRules`](https://ej2.syncfusion.com/documentation/api/form-validator/#addrules)
method and you can also remove an existing rule from the input element by using [`removeRules`](https://ej2.syncfusion.com/documentation/api/form-validator/#removerules)
method.

```typescript

import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import * as React from 'react';

export default class Validation extends React.Component<{}, {}> {
public formObject: FormValidator;

public componentDidMount(): void {
        const options: FormValidatorModel = {
         rules: {
          'email': {
            required: [true, '* Enter your email']
          },
          'mobile': {
            required: [true, '* Enter your mobile number']
          },
          'name': {
              required: [true, '* Enter your name']
          },
        }
      };
      this.formObject = new FormValidator('#form1', options);
      // Add email rule to user element
      this.formObject.addRules('name', { maxLength : [5, 'Character count should not greater than 5'] });
      // Remove number rule from age element
      this.formObject.removeRules('mobile', ['number']);
  }

  public render() {
    return (
      <form id='form1'>
        <div>
          <input type='text' className='e-input' name='email'/>
        </div>
        <div>
          <input type='text' className='e-input' name='name'/>
        </div>
        <div>
          <input type='text' className='e-input' name='mobile'/>
        </div>
      </form>
    )
  }
}

```

## Validating a single Element

The validate method have an optional argument, where you can pass an input element's
name attribute to validate its value against the defined rule.

```typescript

import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import * as React from 'react';

export default class Validation extends React.Component<{}, {}> {
public formObject: FormValidator;

public componentDidMount(): void {
        const options: FormValidatorModel = {
         rules: {
          'email': {
            required: [true, '* Enter your email']
          },
          'mobile': {
            required: [true, '* Enter your mobile number']
          },
          'name': {
              required: [true, '* Enter your name']
          },
        }
      };
      this.formObject = new FormValidator('#form1', options);
      // Add email rule to user element
      this.formObject.validate('name');
  }

  public render() {
    return (
      <form id='form1'>
        <div>
          <input type='text' className='e-input' name='email'/>
        </div>
        <div>
          <input type='text' className='e-input' name='name'/>
        </div>
        <div>
          <input type='text' className='e-input' name='mobile'/>
        </div>
      </form>
    )
  }

}
```