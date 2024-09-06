---
title: "Hide dropdown arrow"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Hide dropdown arrow

You can hide the dropdown arrow from the DropDownButton by adding class `e-caret-hide`
to DropDownButton element using [`cssClass`](../../api/drop-down-button#cssclass)
property.

{% tab template= "drop-down-button/hide", sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];

  public render() {
    return (
    <div>
      <DropDownButtonComponent items = {this.items} cssClass='e-caret-hide'> Clipboard</DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}