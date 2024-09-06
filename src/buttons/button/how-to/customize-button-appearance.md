---
title: "Customize Button Appearance"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Customize Button Appearance

You can customize the appearance of the Button by using the Cascading Style Sheets (CSS).
Define the CSS according to your requirement, and assign the class name to the [`cssClass`](../../api/button#cssclass) property.
In the following code snippet the background color, text color, height, width, and sharp corner of the Button can be
customized through the `e-custom` class for all states (hover, focus, and active).

{% tab template="button/howto", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To customize Button appearance.
// Refer the "e-custom" class details in "styles.css".
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <ButtonComponent cssClass='e-custom'>Custom</ButtonComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}
