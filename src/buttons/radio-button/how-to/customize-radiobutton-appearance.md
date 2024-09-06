---
title: "Customize RadioButton Appearance"
component: "RadioButton"
description: "React RadioButton how to section, name and value in form submit, customize RadioButton appearance."
---

# Customize RadioButton Appearance

You can customize the appearance of the RadioButton component by using the CSS rules.
Define own CSS rules according to your requirement and assign the class name to the [`cssClass`](../../api/radio-button#cssclass) property.

The background and border color of the RadioButton is customized through the custom classes to create the primary, success, warning,
danger, and info type of radio button.

{% tab template="radio-button/howto", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { RadioButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// To customize RadioButton appearance.
class App extends React.Component<{}, {}> {
  public render() {
    return (
        <ul>
            {/* Refer the 'e-primary' class details in 'style.css'.*/}
            <li><RadioButtonComponent label="Primary" cssClass="e-primary" name="custom" /></li>

            {/* Refer the 'e-success' class details in 'style.css'.*/}
            <li><RadioButtonComponent label="Success" cssClass="e-success" name="custom" /></li>

            {/* Refer the 'e-info' class details in 'style.css'.*/}
            <li><RadioButtonComponent label="Info" cssClass="e-info" checked={true} name="custom" /></li>

            {/* Refer the 'e-warning' class details in 'style.css'.*/}
            <li><RadioButtonComponent label="Warning" cssClass="e-warning" name="custom" /></li>

            {/* Refer the 'e-danger' class details in 'style.css'.*/}
            <li><RadioButtonComponent label="Danger" cssClass="e-danger" name="custom" /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}