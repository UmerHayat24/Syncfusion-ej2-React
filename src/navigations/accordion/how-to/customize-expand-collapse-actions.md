---
title: "Accordion animation behavior"
component: "Accordion"
description: "This section explains how to customize the Syncfusion Essential JS 2 Accordion expand and collapse animation action behavior using events."
---

# Customize Accordion expand or collapse animation behavior

Accordion component supports customizing the expand or collapse animation action behavior. You can manually change the expand animation action performed after the collapse animation operation performed on already expand pane when the expand icons are clicked.

By default, the Accordion component pane is expanded or collapsed, when click the expand or collapse icon. It is not affected on already expand pane.

The following sample demonstrates, how to expand the collapsed Accordion item after collapse animation performed on the expanded Accordion item using [`created`](../../api/accordion/#created), [`expanding`](../../api/accordion/#expanding), and [`expanded`](../../api/accordion/#expanded) event. In the Expanding event, get the previously expanded item index and prevent the expanding behavior using `args.cancel` option. Expand the Accordion item dynamically based on specifying the `index` value using the [`expandItem`](../../api/accordion/#expanditem) public method and [`expanded`](../../api/accordion/#expanded) event.

{% tab template="accordion/accordion-actions", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective, ExpandEventArgs } from '@syncfusion/ej2-react-navigations';
import { SampleBase } from './sample-base';

export default class ReactApp extends React.Component<{}, {}> {
  public initialLoad: Boolean = true;
  public isCollapsed: Boolean = false;
  public expandIndex: any;
  public acrdnInstance:AccordionComponent;
  public render() {
    return (
      <AccordionComponent expanded= {this.expanded.bind(this)} expanding= {this.expanding.bind(this)} created= {this.created.bind(this)} expandMode='Single' ref={acrdn => this.acrdnInstance = acrdn}>
              <AccordionItemsDirective>
                <AccordionItemDirective header='ASP.NET' content='Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services. ASP.NET pages execute on the server and generate markup such as HTML, WML, or XML that is sent to a desktop or mobile browser. ASP.NET pages use a compiled,event-driven programming model that improves performance and enables the separation of application logic and user interface.' />
                <AccordionItemDirective header='ASP.NET MVC' content='The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller. The ASP.NET MVC framework provides an alternative to the ASP.NET Web Forms pattern for creating Web applications. The ASP.NET MVC framework is a lightweight, highly testable presentation framework that (as with Web Forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication.' />
                <AccordionItemDirective header='Javascript' content='JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.More recently, however, it has become common in both game development and the creation of desktop applications.' />
              </AccordionItemsDirective>
            </AccordionComponent>
    );
  }
  public expanding (e: ExpandEventArgs) {
      if (e.isExpanded && !this.initialLoad && !this.isCollapsed) {
            e.cancel = true;
            this.expandIndex = this.acrdnInstance.items.indexOf(e.item);
            this.isCollapsed = true;
      }
  }
  public expanded (e: ExpandEventArgs) {
    if (!e.isExpanded && !this.initialLoad && this.isCollapsed) {
           this.acrdnInstance.expandItem(true, this.expandIndex);
           this.isCollapsed = false;
      }
  }
  public created (): void {
     this.initialLoad = false;
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));
```

{% endtab %}