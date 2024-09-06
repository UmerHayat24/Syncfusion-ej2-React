# Error Messages

The `FormValidator` provides default error messages for all default validation rules.
It is tabulated as follows

| Rules | message |
| ------------- | ------------- |
| `required` | This field is required. |
| `email` | Please enter a valid email address. |
| `url` | Please enter a valid URL. |
| `date` | Please enter a valid date. |
| `dateIso` | Please enter a valid date ( ISO ). |
| `number` | Please enter a valid number. |
| `digit` | Please enter only digits. |
| `maxLength` | Please enter no more than {0} characters. |
| `minLength` | Please enter at least {0} characters. |
| `rangeLength` | Please enter a value between {0} and {1} characters long. |
| `range` | Please enter a value between {0} and {1}. |
| `max` | Please enter a value less than or equal to {0}. |
| `min` | Please enter a value greater than or equal to {0}. |
| `regex` | Please enter a correct value. |

## Customizing Error Messages

The default error message for a rule can be customizable by defining it along with concern rule object as follows.

{% tab template="form-validator/error-messages", sourceFiles="app/**/*.tsx" %}

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
  // Dialog will be closed, while clicking on overlay
  public onOverlayClick() {
        this.dialogInstance.hide();
  }
  public componentDidMount(): void {
        const options: FormValidatorModel = {
          // validation rules
         rules: {
          'email': {
            required: [true, '* Enter your email']
          },
          'password': {
            required: [true, '* Enter your password']
          },
        }
      };
      // Initialize the form validator
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
      <div className='validation_wrapper'>
      <div className="control_wrapper" id="control_wrapper">
        <form id="form1"  method="post">
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
              <input type="password" id="number" name="password" data-msg-containerid="noError" />
              <span className="e-float-line"/>
              <label className="e-float-text e-label-top"  htmlFor="password" >Password</label>
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

ReactDOM.render(<Validation />, document.getElementById('form-element'));
```

{% endtab %}
