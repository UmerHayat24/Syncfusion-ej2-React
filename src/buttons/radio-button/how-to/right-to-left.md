---
title: "Right-To-Left"
component: "RadioButton"
description: "React RadioButton how to section, name and value in form submit, customize RadioButton appearance."
---

# Right-To-Left

RadioButton component has RTL support. This can be achieved by setting [`enableRtl`](../../api/radio-button#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in RadioButton component.

{% tab template="radio-button/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { RadioButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render RadioButton.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <ul>
      <li><RadioButtonComponent label="Option 1" name="default" enableRtl={true} /></li>
      <li><RadioButtonComponent label="Option 2" name="default" enableRtl={true} /></li>
      </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}