---
title: "Load Tab items dynamically"
component: "Tab"
description: "This example demonstrates how to dynamically load or add a tab item in the Essential JS 2 Tab control."
---

# Load Tab items dynamically

Tabs can be added dynamically by passing array of items and index value to the [`addTab`](../../api/tab#addtab) method.

```typescript
    // New tab title and content inputs are fetched and stored in local variable
    let title: string = document.getElementById('tab-title').value;
    let content: string = document.getElementById('tab-content').value;

    // Required tab item object formed by using textbox inputs
    let item: Object =  { header: { text: title }, content: createElement('pre', { innerHTML: content.replace(/\n/g, '<br>\n') }).outerHTML };

    // Item object and the index argument passed into the addTab method to add a new tab
    this.addTab([item], this.totalItems-1);
```

In the following demo, you can add the tab content by clicking the **+**.  This **+** icon is added on the tab header using [`iconCss`](../../api/tab/header#iconcss) property.  Enter the new Tab heading and content details in the available text boxes, click 'Add Tab' button to pass the details as an array and here last index is calculated to append the new tab at the end.

{% tab template="tab/dynamic-tab", isDefaultActive=true, compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective, SelectEventArgs } from '@syncfusion/ej2-react-navigations';
import { Tooltip } from '@syncfusion/ej2-popups';
import { enableRipple, createElement } from '@syncfusion/ej2-base';

enableRipple(true);

export default class App extends React.Component<{}, {}> {
  public tabInstance: TabComponent | any;
  public totalItems: number | any;

  public tabCreated(): void {
    const tooltip: Tooltip = new Tooltip({
      content: 'Add Tab'
    });
    tooltip.appendTo('.e-ileft.e-icon');

    (document.getElementById('btn-add') as any).onclick = (e : Event) => {
      const title: string = (document.getElementById('tab-title') as any).value;
      const content: string = (document.getElementById('tab-content') as any).value;
      const ele = document.createElement("pre");
      ele.innerHTML = content.replace(/\n/g, "<br>\n");
// tslint:disable-next-line: ban-types
      const item: Object =  { header: { text: title }, content: ele.outerHTML };
      const totalItems = document.querySelectorAll('#element .e-toolbar-item').length;
      (document.getElementById('tabelement') as any).ej2_instances[0].addTab([item], totalItems-1);
    };
  }

  public tabSelected(args: SelectEventArgs): any {
    if (args.selectedIndex === document.querySelectorAll('#element .e-toolbar-item').length -1) {
      (document.getElementById('tab-title') as any).value = '';
      (document.getElementById('tab-content') as any).value = '';
    }
  }

  public render() {
    let headertext: any;
    headertext = [{ text: "Twitter"}, { 'iconCss': 'e-add-icon' } ];

    return (
      <TabComponent id='tabelement' ref={tab => this.tabInstance = tab} created={this.tabCreated}  selected={this.tabSelected.bind(this)}>
        <TabItemsDirective>
          <TabItemDirective header= { headertext[0] } content= { '#tab1_content' } />
          <TabItemDirective header= { headertext[1] } content= { '#form-container' } />
        </TabItemsDirective>
      </TabComponent>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
