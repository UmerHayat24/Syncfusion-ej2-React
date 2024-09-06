---
title: "Right-To-Left"
component: "CheckBox"
description: "React CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Right-To-Left

CheckBox component has RTL support. This can be achieved by setting [`enableRtl`](../../api/check-box#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in CheckBox component.

{% tab template="check-box/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);
// To customize CheckBox appearance.
class App extends React.Component<{}, {}> {
  public render() {
    return (
        <ul>
            <li><CheckBoxComponent label="Default" enableRtl={true} /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}