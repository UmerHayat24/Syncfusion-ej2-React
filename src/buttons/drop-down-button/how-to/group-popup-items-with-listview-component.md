---
title: "Group popup items with ListView component"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Group popup items with ListView component

Header in popup items is possible in DropdownButton by templating entire popup with ListView.
Create ListView with id `#listview` and provide it as a
[`target`](../../api/drop-down-button#target) for DropDownButton.

In the following example, ListView element is given as `target` to DropDownButton and header
can be achieved by [`groupBy`](../../api/list-view/fieldSettings#groupby) property.

{% tab template= "drop-down-button/header", sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { DropDownButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {
  public data: Array<{ [key: string]: string; }> = [
    { class: 'data', text: 'Print', id: 'data1', category: 'Customize Quick Access Toolbar' },
    { class: 'data', text: 'Save As', id: 'data2', category: 'Customize Quick Access Toolbar' },
    { class: 'data', text: 'Update Folder', id: 'data3', category: 'Customize Quick Access Toolbar' },
    { class: 'data', text: 'Reply', id: 'data4', category: 'Customize Quick Access Toolbar' }
  ];

  public field: { [key: string]: string; } = { text: 'text', groupBy: 'category' };
  
  public render() {
    return (
      <div>
        <ListViewComponent id="listview" dataSource={this.data} fields={this.field} showCheckBox={true}/>
        <DropDownButtonComponent  target='#listview' iconCss='e-icons e-down' cssClass='e-caret-hide'/>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}