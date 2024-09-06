---
title: "Localization"
component: "FromValidator"
description: "Localization support in FromValidator"
---

# Localization

The [`Localization`](../common/localization/) library allows users to localize the default error message contents of the `formValidator` to different cultures using the `locale` property.

The FormValidator provides default error messages for all default validation rules. It is tabulated as follows:

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

## Loading translations

To load translation object in your application use `load` function of `L10n` class.

The following example demonstrates the FormValidator in `Arabic` culture with error message for email.

{% tab template="form-validator/localization", sourceFiles="app/**/*.tsx" %}

```typescript
import { L10n, select } from '@syncfusion/ej2-base';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

L10n.load({
     'ar-AR': {
        'formValidator':{
            "creditcard": "يرجى إدخال رقم بطاقة صالح",
            "date": "ارجوك ادخل تاريخ صحيح.",
            "dateIso": "الرجاء إدخال تاريخ صالح (ISO)",
            "digits" : "الرجاء إدخال الأرقام فقط",
            "email": "أدخل بريد إلكتروني صالح",
            "equalTo" : "يرجى إدخال نص مطابقة صحيح",
            "max" : "الرجاء إدخال قيمة أقل من أو تساوي {0}",
            "maxLength" : "الرجاء إدخال ما لا يزيد عن {0} حرف",
            "min" : "الرجاء إدخال قيمة أكبر من أو تساوي {0}",
            "minLength": "الرجاء إدخال أحرف {0} على الأقل",
            "number" : "من فضلك أدخل رقما صالحا",
            "pattern" : "الرجاء إدخال قيمة نمط صحيح",
            "range" : "يرجى إدخال قيمة بين {0} و {1}",
            "rangeLength" : "يرجى إدخال قيمة بين {0} و {1} من الأحرف",
            "regex": "يرجى إدخال قيمة صحيحة",
            "required" : "هذه الخانة مطلوبه",
            "tel" : "يرجى إدخال رقم هاتف صالح",
            "url": "أدخل رابط صحيح من فضلك"
        }
    }
});


export default class Validation extends React.Component<{}, {}> {
public dialogInstance: DialogComponent;
public formObject: FormValidator;

  // Dialog will be closed, while clicking on overlay
  public onOverlayClick() {
        this.dialogInstance.hide();
  }
  public componentDidMount(): void {
        const options: FormValidatorModel = {
          locale:"ar-AR",
          rules: {
          email: { email: true },
        }
      };
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
                        </form>
                      </div>
                    </div>
                  </div>
                </div>) }
}
ReactDOM.render(<Validation />, document.getElementById('form-element'));
```

{% endtab %}
