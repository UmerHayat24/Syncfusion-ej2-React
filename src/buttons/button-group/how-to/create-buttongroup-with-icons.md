---
title: "Create ButtonGroup with icons"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Create ButtonGroup with icons

ButtonGroup with icons can be achieved by using `iconCss` property of the Button component.

The following example illustrates how to create ButtonGroup with icons.

{% tab template="button-group/icon", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ButtonGroup with icons.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className='e-btn-group'>
          <ButtonComponent iconCss='e-icons e-left-icon'>HTML</ButtonComponent>
          <ButtonComponent iconCss='e-icons e-middle-icon'>CSS</ButtonComponent>
          <ButtonComponent iconCss='e-icons e-right-icon'>Javascript</ButtonComponent>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));
```

{% endtab %}