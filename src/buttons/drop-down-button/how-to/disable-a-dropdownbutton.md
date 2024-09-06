---
title: "Disable a DropDownButton"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Disable a DropDownButton

DropdownButton component can be enabled/disabled by giving [`disabled`](../../api/drop-down-button#disabled) property.
To disable DropdownButton component, the disabled property can be set as `true`.

{% tab template= "drop-down-button/disabled", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

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
        text: 'Edit'
    },
    {
        text: 'Delete'
    },
    {
        text: 'Mark as Read'
    },
    {
        text: 'Like Message'
    }];

  public render() {
    return (
    <div>
      <DropDownButtonComponent items = {this.items} iconCss= 'ddb-icons e-message' disabled={true}> Message </DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}