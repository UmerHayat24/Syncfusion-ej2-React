---
title: "Integrate Essential JS 2 TreeView inside the Accordion"
component: "Accordion"
description: "This example demonstrates how to integrate the Essential JS 2 TreeView control inside the Essential JS 2 Accordion control."
---

# Integrate Essential JS 2 TreeView inside the Accordion

Accordion supports to render other Essential JS 2 Components by using content property.
You can give content as an element string like below, for initializing the component.

```js
content: '<div id="element"> </div>'
```

The other component can be rendered with the use of provided events, such as [`clicked`](../../api/accordion#clicked) and [`expanding`](../../api/accordion#expanding).
The following procedure is to render a TreeView within the Accordion,

* Import the `TreeView` module from `ej2-navigations`, for adding TreeView. Please refer the [TreeView initialization steps](../../../treeview/getting-started.html)

* You can initialize the TreeView component in [`expanding`](../../api/accordion#expanding) event, by getting the element and defining the required TreeView properties.

{% tab template="accordion/accordion-treeview", compileJsx=true %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-react-navigations';
import { Accordion, ExpandEventArgs, TreeView } from '@syncfusion/ej2-navigations';
import { DocDB, DownloadDB, PicDB } from 'datasource.ts';

let clickEle: HTMLElement;
class ReactApp extends React.Component<{}, {}> {
  public acrdnInstance:AccordionComponent;
  render() {
       return (
        <AccordionComponent  ref={acrdn => this.acrdnInstance = acrdn}  expandMode='Single' expanding= {this.expanding.bind(this)}>
            <AccordionItemsDirective>
              <AccordionItemDirective header='Documents' content='<div id="treeDoc"></div>'  />
              <AccordionItemDirective header='Downloads' content='<div id="treeDownload"></div>' />
              <AccordionItemDirective header='Pictures' content='<div id="treePic"></div>' />
            </AccordionItemsDirective>
        </AccordionComponent>
       );
  }
  public expanding (e: ExpandEventArgs) {
  if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 0 && e.element.querySelector('#treeDoc').childElementCount === 0) {
        let treeObj: TreeView = new TreeView({
        fields: { dataSource: DocDB, id: 'nodeId', text: 'nodeText', child: 'nodeChild', iconCss: 'icon', imageUrl: 'image' },
        sortOrder: 'Ascending'
    });
    treeObj.appendTo('#treeDoc');
  }
    if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 1 && e.element.querySelector('#treeDownload').childElementCount === 0) {
        let treeObj: TreeView = new TreeView({
        fields: { dataSource: DownloadDB, id: 'nodeId', text: 'nodeText', child: 'nodeChild', iconCss: 'icon', imageUrl: 'image' },
        sortOrder: 'Ascending'
    });
    treeObj.appendTo('#treeDownload');
  }
      if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 2 && e.element.querySelector('#treePic').childElementCount === 0) {
        let treeObj: TreeView = new TreeView({
        fields: { dataSource: PicDB, id: 'nodeId', text: 'nodeText', child: 'nodeChild', iconCss: 'icon', imageUrl: 'image' },
        sortOrder: 'Ascending'
    });
    treeObj.appendTo('#treePic');
  }
   }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));

```

{% endtab %}