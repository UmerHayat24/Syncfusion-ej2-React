---
title: "Set text on Switch"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit, text."
---

# Set text on Switch

This section explains how to set [`onLabel`](https://ej2.syncfusion.com/react/documentation/api/switch/#onlabel)
and [`offLabel`](https://ej2.syncfusion.com/react/documentation/api/switch/#offlabel) texts on Switch. In the following example, `onLabel` is set as
`ON` and `offLabel` is set as `OFF`.

{% tab template="switch/text", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render Switch.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <SwitchComponent onLabel="ON" offLabel="OFF" checked={true}  />
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}

> Switch does not have text support for material themes, and does not support long custom text.
