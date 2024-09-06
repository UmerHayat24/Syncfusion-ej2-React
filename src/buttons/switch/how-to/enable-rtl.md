---
title: "Enable RTL"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Enable RTL

Switch component has RTL support. This can be achieved by setting [`enableRtl`](../../api/switch#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in Switch component.

{% tab template= "switch/getting-started", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Switch with checked state.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <SwitchComponent enableRtl={true} checked={true} />
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}