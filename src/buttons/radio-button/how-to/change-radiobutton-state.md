---
title: "Change RadioButton State"
component: "RadioButton"
description: "React RadioButton how to section, name and value in form submit, customize RadioButton appearance, change RadioButton state."
---

# Change the RadioButton state

The Essential JS 2 RadioButton contains 2 different states visually, they are as follows:
* Checked
* Unchecked

The RadioButton [`checked`](https://ej2.syncfusion.com/react/documentation/api/radio-button/#checked) property is used to handle
the checked and unchecked state. In the checked state an inner circle will be added to the visualization of RadioButton.

{% tab template= "radio-button/label-and-size", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { RadioButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <ul>
            {/* checked state. */}
            <li><RadioButtonComponent label="Option 1" name="state" checked={true} /></li>

            {/* unchecked state. */}
            <li><RadioButtonComponent label="Option 2" name="state" /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}