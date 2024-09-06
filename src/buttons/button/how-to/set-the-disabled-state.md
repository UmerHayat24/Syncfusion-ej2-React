---
title: "Set the disabled state"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Set the disabled state

Button component can be enabled/disabled by giving [`disabled`](../../api/button#disabled) property. To disable Button component,
the `disabled` property can be set as `true`.

The following example demonstrates Button in `disabled` state.

{% tab template="button/default", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div>
            <ButtonComponent disabled={true}>Disabled</ButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}