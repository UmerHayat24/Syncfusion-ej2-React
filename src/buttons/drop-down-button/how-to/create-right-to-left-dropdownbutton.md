---
title: "Create right-to-left DropDownButton"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Create right-to-left DropDownButton

DropDownButton component has RTL support. This can be achieved by setting [`enableRtl`](../../api/drop-down-button#enablertl) as true.

The following example illustrates how to enable right-to-left support in DropDownButton component.

{% tab template= "drop-down-button/disabled",  sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

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
      <DropDownButtonComponent items = {this.items} iconCss= 'ddb-icons e-message' enableRtl={true}> Message </DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}