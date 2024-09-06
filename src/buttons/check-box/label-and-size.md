---
title: "CheckBox Label and Size"
component: "CheckBox"
description: "React CheckBox component supports different sizes and label."
---

# Label and Size

This section explains the different sizes and labels.

## Label

The CheckBox caption can be defined using the [`label`](../api/check-box#label) property.
This reduces manual addition of label for CheckBox. You can customize the label position before or after the CheckBox
through the [`labelPosition`](../api/check-box#labelposition) property.

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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
            {/* Label position - Left. */}
            <li><CheckBoxComponent label="Left Side Label" labelPosition="Before" /></li>

            {/* Label position - Right. */}
            <li><CheckBoxComponent label="Right Side Label" checked={true} /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}

## Size

The different CheckBox sizes available are default and small. To reduce size of the default CheckBox to small,
set the [`cssClass`](../api/check-box#cssclass) property to `e-small`.

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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
            {/* Small CheckBox. */}
            <li><CheckBoxComponent label="Small" cssClass="e-small" /></li>

            {/* Default CheckBox. */}
            <li><CheckBoxComponent label="Default" /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}

## See Also

* [CheckBox customization](./how-to/customized-checkbox)