---
title: "CheckBox States"
component: "CheckBox"
description: "React CheckBox component supports three different states."
---

# CheckBox States

The Essential JS 2 CheckBox contains 3 different states visually, they are:
* Checked
* Unchecked
* Indeterminate

## Checked and Unchecked

The CheckBox [`checked`](../api/check-box#checked) property is used to handle the checked and unchecked state. In checked state a tick mark will be added to the visualization of CheckBox.

## Indeterminate

The CheckBox indeterminate state can be set through [`indeterminate`](../api/check-box#indeterminate) property.
CheckBox indeterminate state masks the real value of CheckBox visually. The Checkbox cannot be changed to indeterminate state through
the user interface, this state can be achieved only through the property.

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <ul>
            {/* checked state. */}
            <li><CheckBoxComponent label="Checked State" checked={true} /></li>

            {/* unchecked state. */}
            <li><CheckBoxComponent label="Unchecked State" /></li>

            {/* indeterminate state. */}
            <li><CheckBoxComponent label="Indeterminate State" indeterminate={true} /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}