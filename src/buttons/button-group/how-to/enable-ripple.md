---
title: "Enable ripple"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Enable ripple

Ripple can be enabled by importing `enableRipple` method from `ej2-base` and set enableRipple as `true`.

The following example illustrates how to enable ripple for ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To enable ripple in ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className='e-btn-group'>
          <ButtonComponent>HTML</ButtonComponent>
          <ButtonComponent>CSS</ButtonComponent>
          <ButtonComponent>Javascript</ButtonComponent>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}