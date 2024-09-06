---
title: "Disable"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Disable

## Particular button

To disable a particular button in a ButtonGroup, [`disabled`](../../api/button#disabled) attribute should be added to corresponding button element.

## Whole ButtonGroup

To disable whole ButtonGroup, `disabled` attribute should be added to all the button elements.

The following example illustrates how to disable the particular and the whole ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To disable single button/whole ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
      return (
        <div>
          <div className='e-btn-group'>
            <ButtonComponent>HTML</ButtonComponent>
            <ButtonComponent disabled = {true}>CSS</ButtonComponent>
            <ButtonComponent>Javascript</ButtonComponent>
          </div>
          <div className='e-btn-group'>
            <ButtonComponent disabled = {true}>HTML</ButtonComponent>
            <ButtonComponent disabled = {true}>CSS</ButtonComponent>
            <ButtonComponent disabled = {true}>Javascript</ButtonComponent>
          </div>
        </div>
      );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}

> To disable radio/checkbox type ButtonGroup, the `disabled` attribute should be added to the particular input element.