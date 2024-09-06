---
title: "Tooltip for Button"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Tooltip for Button

Tooltip can be shown on Button hover and it can be achieved by setting `title` attribute.

The following snippets illustrates how to show tooltip on Button hover.

{% tab template="button/howto", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import {ButtonComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public btn: ButtonComponent;
    constructor(props: any) {
      super(props);
      this.onCreated = this.onCreated.bind(this);
    }
    public onCreated(): void {
      (this.btn.element as HTMLElement).setAttribute('title','Primary Button');
    }
    public render() {
      return (
          <div>
              <ButtonComponent id='btn' ref={(scope) => { this.btn = scope as ButtonComponent; }} created={this.onCreated} isPrimary={true}>Button</ButtonComponent>
          </div>
      );
    }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}