---
title: "Rich text editor Validation"
component: "Rich Text Editor"
description: "This section explains on how to validate the Syncfusion react Rich Text Editor's value  by applying validationRules and validationMessage."
---

# Validation

## Validation rules

The Rich Text Editor provides the functionality of character count and its validation. So, you can validate the Rich Text Editor’s value on form submission by applying validationRules and validationMessage to the Rich Text Editor.

| **Rules** | **Description** |
| --- | --- |
| required | Requires the value for the Rich Text Editor control. |
| minlength | Requires the value to be of given minimum characters count. |
| maxlength | Requires the value to be of given maximum characters count. |

This sample is used to validate form using the obtrusive Validation. Type the values in Rich Text Editor and the form enables the validation with the formvalidator rules by clicking on the submit externally. All rules are validated by the formvalidator rules.

## Validation message

The default error message for a rule can be customizable by defining it along with the concern rule object as follows.

In the following sample, customize the error message along with the concern rule.

{% tab template="rich-text-editor/form", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Form Validation Sample
 */
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { HtmlEditor, Image, Count, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public formObject: FormValidator;
  public componentDidMount(): void {
    const option: FormValidatorModel = {
      rules: {
        defaultRTE: {
          maxLength:[108, 'Maximum 100 character only'],
          minLength: [15, 'Need atleast 8 character length'],
          required: true
        }
      }
    };
    this.formObject = new FormValidator('#myForm', option);

    (document as any).getElementById('validateSubmit').addEventListener('click', (e: any) => {
      const form = (document.forms as any).myForm;
      const formData = new FormData(form);
      const rteValue = formData.get('defaultRTE');
      // Use this value to the data base.
      alert(rteValue);
      e.preventDefault();
    });
  }
 private onChange(): void {
       this.button.disabled = false;
    }
  public render() {
    return (
      <form id="myForm" className="form-vertical">
        <div className="form-group">
          <RichTextEditorComponent id="defaultRTE" name="defaultRTE" className="form-control" height={200} showCharCount={true} maxLength={100} placeholder={'Type something'}  change={this.onChange.bind(this)} value={''}>
            <Inject services={[Toolbar, Image, Link, Count, HtmlEditor, QuickToolbar]} />
          </RichTextEditorComponent>
        </div>
        <div className="form-btn-section">
          <ButtonComponent id="validateSubmit" ref={(scope) => { this.button = scope; }}  disabled={true}>Submit</ButtonComponent>
          <button id="reset-btn" className="sample-btn e-control e-btn" type="reset" data-ripple="true">Reset</button>
        </div>
      </form>
    );
  }
}

export default App;

```

{% endtab %}

## Custom placement of validation message

The FormValidator has an event customPlacement which can be used to place the error message from default position to desired custom location.

{% tab template="rich-text-editor/form", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Custom Placement of Validation Message Sample
 */
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { HtmlEditor, Image, Inject, Count , Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public formObject: FormValidator;
  public componentDidMount(): void {
    const option: FormValidatorModel = {
      customPlacement: (inputElement: HTMLElement, error: HTMLElement)=> {
        // Initialize the CustomPlacement.
        (document as any).getElementById('data-error').appendChild(error);
      },
      rules: {
        defaultRTE: {
          maxLength:[108, 'RTE: Maximum 100 character only'],
          minLength: [15, 'RTE: Need atleast 8 character length'],
          required: [true, 'RTE: value is required']
        }
      }
    };
    this.formObject = new FormValidator('#myForm', option);

    (document as any).getElementById('validateSubmit').addEventListener('click', (e: any) => {
      const form = (document as any).forms.myForm;
      const formData = new FormData(form);
      const rteValue = formData.get('defaultRTE');
      // Use this value to the data base.
      alert(rteValue);
      e.preventDefault();
    });
  }

  private onChange(): void {
     this.button.disabled = false;
    }

  public render() {
    return (
      <form id="myForm" className="form-vertical">
        <div className="form-group">
          <RichTextEditorComponent id="defaultRTE" name="defaultRTE" className="form-control" height={200} showCharCount={true} maxLength={100} placeholder={'Type something'} change={this.onChange.bind(this)} value={''}>
            <Inject services={[Toolbar, Image, Link, Count, HtmlEditor, QuickToolbar]} />
          </RichTextEditorComponent>
        </div>
        <div className="form-group">
          <div className="col-sm-3 control-label"/>
          <div className="col-sm-6">
            <div id='data-error'/>
          </div>
        </div>
        <div className="form-btn-section">
            <ButtonComponent id="validateSubmit" ref={(scope) => { this.button = scope; }}  disabled={true}>Submit</ButtonComponent>
          <button id="reset-btn" className="sample-btn e-control e-btn" type="reset" data-ripple="true">Reset</button>
        </div>
      </form>
    );
  }
}

export default App;

```

{% endtab %}