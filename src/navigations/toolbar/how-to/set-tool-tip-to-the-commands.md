---
title: "Set Essential JS 2 Tooltip to the commands"
component: "Toolbar"
description: "This example demonstrates how to set the Essential JS 2 Tooltip control to the Essential JS 2 Toolbar control commands."
---

# Set Essential JS 2 tooltip to the commands

The [`tooltipText`](../../api/toolbar/item#tooltiptext) property of the Toolbar item is used to set the HTML Tooltip to the commands that can be viewed as hint texts on mouse hover.

To change the [`tooltipText`](../../api/toolbar/item#tooltiptext) to ej2-tooltip component:

* Import the `Tooltip` module from `ej2-popups`,and initialize the Tooltip with the Toolbar target. Refer to the following code example:

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Tooltip } from '@syncfusion/ej2-popups';
import { ToolbarComponent, ItemsDirective, ItemDirective } from '@syncfusion/ej2-react-navigations';

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
           <div id="Tooltip">
           <ToolbarComponent width="300">
           <ItemsDirective>
              <ItemDirective text="Cut" tooltipText="Cut"/>
              <ItemDirective text="Copy" tooltipText="Copy"/>
              <ItemDirective text="Paste" tooltipText="Paste"/>
              <ItemDirective text="Undo" tooltipText="Undo"/>
              <ItemDirective text="Redo" tooltipText="Redo"/>
           </ItemsDirective>
           </ToolbarComponent></div>
       );
  }
  componentDidMount() {
   let tooltip: Tooltip = new Tooltip({
   target: '#toolbar [title]',
   });
   tooltip.appendTo('#Tooltip');
   }
}
ReactDOM.render(<ReactApp/>, document.getElementById("toolbar"));

```

{% endtab %}