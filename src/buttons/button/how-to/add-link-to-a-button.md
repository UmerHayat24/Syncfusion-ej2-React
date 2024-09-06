---
title: "Add link to a Button"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Add link to a Button

The appearance of the Button can be changed like a link by `e-link` class using [`cssClass`](../../api/button#cssclass)
property and link navigation can be handled in Button click.

In the following example, link is added in Button click by using `window.open()` method.

{% tab template="button/default", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    // Click Event.
    public btnClick (): void {
      window.open("https://www.google.com");
    }
    public render() {
        return (
            <div>
                <ButtonComponent cssClass='e-link' onClick={this.btnClick.bind(this)}>Go to google</ButtonComponent>
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}