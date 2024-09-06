---
title: "To keep single pane open always"
component: "Accordion"
description: "This example demonstrates how to keep a single pane in an expanded state in the Essential JS 2 Accordion control."
---

# To keep single pane open always

By default, all Accordion panels are collapsible. You can customize the Accordion to keep one panel as
expanded state always. This is applicable for `Single` expand mode.

{% tab template="accordion/accordion", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-react-navigations';
import { ExpandEventArgs, AccordionClickArgs} from '@syncfusion/ej2-navigations';

let clickEle: HTMLElement;
class ReactApp extends React.Component<{}, {}> {
  public acrdnInstance:AccordionComponent;
  public clickEle;
  render() {
       this.clickEle = this.props.data;
       return (
        <AccordionComponent  ref={acrdn => this.acrdnInstance = acrdn}  expandMode='Single' clicked= {this.clicked.bind(this)}  expanding= {this.expanding.bind(this)}>
            <AccordionItemsDirective>
              <AccordionItemDirective expanded='true' header='ASP.NET' content='Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.' />
              <AccordionItemDirective header='ASP.NET MVC' content='The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.' />
              <AccordionItemDirective header='JavaScript' content= 'JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.' />
            </AccordionItemsDirective>
        </AccordionComponent>
       );
  }
  public expanding (e: ExpandEventArgs) {
  if (this.acrdnInstance) {
  let expandCount: number = this.acrdnInstance.element.querySelectorAll('.e-selected').length;
  let ele: HTMLElement= this.acrdnInstance.element.querySelectorAll('.e-selected')[0];
  if (ele) {
    ele = ele.firstChild
  }
  if (expandCount === 1 && ele === this.clickEle) {
    e.cancel = true;
  } }
   }
  public clicked (e: AccordionClickArgs ) {
    this.clickEle = e.originalEvent.target
  }
}
ReactDOM.render(<ReactApp data={clickEle}/>, document.getElementById("element"));
```

{% endtab %}
