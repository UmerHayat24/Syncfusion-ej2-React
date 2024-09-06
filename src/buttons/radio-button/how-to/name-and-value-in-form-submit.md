---
title: "Name and Value in form submit"
component: "RadioButton"
description: "React RadioButton how to section, name and value in form submit, customize RadioButton appearance."
---

# Name and Value in form submit

The [`name`](../../api/radio-button#name) attribute of the RadioButton is used to group RadioButton. When the RadioButton are grouped in form, the checked items [`value`](../../api/radio-button#value) attribute
will be post to server on form submit that can be retrieved through the name. The disabled and unchecked RadioButton
value will not be sent to the server on form submit.

In the following code snippet, Credit / Debit card is in checked state.
Now, the value that is in checked state will be sent on form submit.

{% tab template="radio-button/form", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { RadioButtonComponent, ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// Name and Value attribute in form submit.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <form>
        <ul>
            <li><RadioButtonComponent name="payment" value="credit/debit" label="Credit /Debit card" checked={true} /></li>

            <li><RadioButtonComponent name="payment" value="netbanking" label="Net Banking" /></li>

            <li><RadioButtonComponent name="payment" value="cashondelivery" label="Cash On Delivery" /></li>

            <li><RadioButtonComponent name="payment" value="others" label="Others" /></li>

            <li><ButtonComponent isPrimary={true}>Submit</ButtonComponent></li>
        </ul>
      </form>
    );
  }
}
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}