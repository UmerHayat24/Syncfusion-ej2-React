---
title: "RadioButton Label and Size"
component: "RadioButton"
description: "React RadioButton component supports different sizes and label."
---

# Label and Size

This section explains the different sizes and labels.

## Label

RadioButton caption can be defined by using the [`label`](../api/radio-button#label) property.
This reduces the manual addition of label for RadioButton. You can customize the label position before or after the RadioButton
through the [`labelPosition`](../api/radio-button#labelposition) property.

{% tab template= "radio-button/label-and-size", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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
            {/* Label position - Left. */}
            <li><RadioButtonComponent label="Left Side Label" name="position" labelPosition="Before" /></li>

            {/* Label position - Right. */}
            <li><RadioButtonComponent label="Right Side Label" name="position" checked={true} /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}

## Size

The different RadioButton sizes available are default and small. To reduce the size of the default RadioButton to small,
set the [`cssClass`](../api/radio-button#cssclass) property to `e-small`.

{% tab template= "radio-button/label-and-size", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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
            {/* Small RadioButton. */}
            <li><RadioButtonComponent label="Small" name="size" cssClass="e-small" /></li>

            {/* Default RadioButton. */}
            <li><RadioButtonComponent label="Default"  name="size" /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}

## See Also

* [How to customize the RadioButton appearance](./how-to/customize-radiobutton-appearance)
