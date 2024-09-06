---
title: "Accordion Expand mode"
component: "Accordion"
description: "The Accordion control supports expand mode options, that specify the types of expand mode while expanding or collapsing an item."
---

# ExpandMode

 The Accordion supports the two listed types of expand modes while expanding or collapsing the item.

* Single
* Multiple

## Single

The property enables to expand only one Accordion item at a time.
If you expand any new item, the previously expanded one is collapsed and new item changed to expanded state.

You can also choose which accordion pane is expanded state at initial rendering by enabling the [`expanded`](../../api/accordion/accordionItemModel#expanded) property on accordion items.

{% tab template="accordion/accordion", compileJsx=true %}

```typescript
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective  } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public content0() {
    return <div>
        Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.
      </div>;
  }
  public content1() {
    return <div>
        The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.
      </div>;
  }
  public content2() {
    return <div>
        JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.
      </div>;
  }
  public render() {
    return (
        <AccordionComponent expandMode='Single'>
            <AccordionItemsDirective>
              <AccordionItemDirective expanded='true' header='ASP.NET' content={this.content0} />
              <AccordionItemDirective header='ASP.NET MVC' content={this.content1} />
              <AccordionItemDirective header='JavaScript' content={this.content2} />
            </AccordionItemsDirective>
        </AccordionComponent>
    );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## Multiple

Default [`expandMode`](../../api/accordion#expandmode) of the Accordion is `Multiple`. It enables you to expand more than one Accordion item at a time.
 Expand/collapse action can also be toggled by clicking on it again. For example, expanded item is collapsed when you click on it again.

{% tab template="accordion/accordion", compileJsx=true  %}

```typescript
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective  } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public content0() {
    return <div>
        Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services.
      </div>;
  }
  public content1() {
    return <div>
        The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller.
      </div>;
  }
  public content2() {
    return <div>
        JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.
      </div>;
  }
  public render() {
    return (
        <AccordionComponent expandMode='Multiple'>
            <AccordionItemsDirective>
              <AccordionItemDirective expanded='true' header='ASP.NET' content={this.content0} />
              <AccordionItemDirective header='ASP.NET MVC' content={this.content1} />
              <AccordionItemDirective header='JavaScript' content={this.content2} />
            </AccordionItemsDirective>
        </AccordionComponent>
    );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## See Also

* [How to keep single pane open always](./how-to/to-keep-single-pane-open-always/)