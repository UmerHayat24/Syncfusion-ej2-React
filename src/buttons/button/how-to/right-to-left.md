---
title: "Right-To-Left"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Right-To-Left

Button component has RTL support. This can be achieved by setting [`enableRtl`](../../api/button#enablertl) as
`true`.

The following example illustrates how to enable right-to-left support in Button component.

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
            <ButtonComponent enableRtl={true} iconCss='e-btn-icons e-setting-icon'>Settings</ButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}