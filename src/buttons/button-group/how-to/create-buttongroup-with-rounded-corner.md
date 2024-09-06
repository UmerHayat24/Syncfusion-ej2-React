---
title: "Create ButtonGroup with rounded corner"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Create ButtonGroup with rounded corner

The ButtonGroup with rounded corner has round edges on both side. In the ButtonGroup with rounded corner, `e-round-corner` class is to be
added to the target element.

The following example illustrates how to create ButtonGroup with rounded corner.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ButtonGroup with rounded corner.
class App extends React.Component<{}, {}> {
  render() {
    return (
      <div>
        <div className='e-btn-group e-round-corner'>
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