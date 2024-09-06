---
title: "Create a rounded button"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Create a rounded button

Button with rounded corner can be achieved by adding `border-radius` property.

In the following example, `e-round-corner` class is added with `border-radius` as `5px`.

{% tab template="button/round-button", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Button.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <ButtonComponent cssClass='e-round-corner'>Button</ButtonComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}