---
title: "Toggle between the states"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit, toggle between the states."
---

# Change switch state using toggle method

This section explains about how to toggle between the switch states using [`toggle`](../../api/switch/#toggle) method.

{% tab template= "switch/getting-started", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Switch with checked state.
class App extends React.Component<{}, {}> {
  public switch: SwitchComponent;
  constructor(props: any) {
    super(props);
    this.created = this.created.bind(this);
  }

  public created(): void {
    this.switch.toggle();
  }

  public render() {
    return (
      <SwitchComponent id="switch" ref={(scope) => { this.switch = scope as SwitchComponent; }} enableRtl={true} checked={true} created={this.created}/>
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}

> Switch triggers [`change`](../../api/switch/#change) event on every state stage to perform custom operations.