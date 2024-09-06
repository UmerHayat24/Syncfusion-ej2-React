---
title: "Create a Block Button"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Create a Block Button

You can customize a Button into a Block Button that will span the entire width of its parent
element. To create a Block Button, set the [`cssClass`](../../api/button#cssclass) property to `e-block`.

{% tab template="button/block", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div>
            {/* Block Button. */}
            <ButtonComponent cssClass='e-block'>Block Button</ButtonComponent>

            {/* Primary Block Button. */}
            <ButtonComponent cssClass='e-block' isPrimary={true}>Block Button</ButtonComponent>

            {/* Success Block Button. */}
            <ButtonComponent cssClass='e-block e-success'>Block Button</ButtonComponent>
        </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}