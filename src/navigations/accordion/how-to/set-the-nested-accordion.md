---
title: "Set the nested accordion"
component: "Accordion"
description: "This example demonstrates how to create an Essential JS 2 Accordion control inside another Essential JS 2 Accordion control."
---

# Set the nested Accordion

Accordion supports to render `nested` level of Accordion by using [`content`](https://ej2.syncfusion.com/react/documentation/api/accordion/accordionItemModel/#content) property. You can give nested
Accordion content inside the parent Accordion content property by using `id` of nested element. The
nested Accordion can be rendered with the use of provided events, such as [`clicked`](https://ej2.syncfusion.com/react/documentation/api/accordion/#clicked) and [`expanding`](https://ej2.syncfusion.com/react/documentation/api/accordion/#expanding).

{% tab template="accordion/accordion", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective, ExpandEventArgs } from '@syncfusion/ej2-react-navigations';

class ReactApp extends React.Component<{}, {}> {
public acrdnInstance:AccordionComponent;
  render() {
       return (
        <AccordionComponent expanding= {this.expanding.bind(this)} ref={acrdn => this.acrdnInstance = acrdn} >
            <AccordionItemsDirective>
              <AccordionItemDirective header='Video' content='<div id="nested_video"></div>' />
              <AccordionItemDirective header='Music' content='<div id="nested_music"></div>' />
              <AccordionItemDirective header='Images' content= '<div id="nested_images"></div>' />
            </AccordionItemsDirective>
        </AccordionComponent>
       );
  }
  public nestedExpand (e: ExpandEventArgs) {
    if (e.element.querySelectorAll('.e-accordion').length > 0) {
      return;
    }
  ReactDOM.render(<AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective header='New Track1'/>
              <AccordionItemDirective header='New Track2'/>
            </AccordionItemsDirective>
        </AccordionComponent>, document.getElementById("nested_musicNew") as HTMLElement);
  }
  public expanding (e: ExpandEventArgs) {
  if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 0) {
    if (e.element.querySelectorAll('.e-accordion').length > 0) {
      return;
    }
  ReactDOM.render(<AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective header='Video Track1'/>
              <AccordionItemDirective header='Video Track2'/>
            </AccordionItemsDirective>
        </AccordionComponent>, document.getElementById("nested_video") as HTMLElement);
  } else if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 1) {
    if (e.element.querySelectorAll('.e-accordion').length > 0) {
      return;
    }
  ReactDOM.render(<AccordionComponent expanding= {this.nestedExpand}>
            <AccordionItemsDirective>
              <AccordionItemDirective header='Music Track1'/>
              <AccordionItemDirective header='Music Track2'/>
              <AccordionItemDirective header='Music New' content='<div id="nested_musicNew"></div>'/>
            </AccordionItemsDirective>
        </AccordionComponent>, document.getElementById("nested_music") as HTMLElement);
  } else if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 2) {
    if (e.element.querySelectorAll('.e-accordion').length > 0) {
      return;
    }
  ReactDOM.render(<AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective header='Track1'/>
              <AccordionItemDirective header='Track2'/>
            </AccordionItemsDirective>
        </AccordionComponent>, document.getElementById("nested_images") as HTMLElement);
  }
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element") as HTMLElement);
```

{% endtab %}