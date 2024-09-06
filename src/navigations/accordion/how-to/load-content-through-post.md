---
title: "Load content through Ajax"
component: "Accordion"
description: "This example demonstrates how to load the external content into the Essential JS 2 Accordion content through Ajax post."
---

# Load content through Ajax

Accordion supports to load external contents through `AJAX` library. Refer the below steps.

* Import the `Ajax` module from `ej2-base` and initialize with URL path.

* Get data from the Ajax Success event to initialize Accordion with retrieved external path data.

{% tab template="accordion/accordion-ajax", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Ajax } from '@syncfusion/ej2-base';
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-react-navigations';

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <AccordionComponent>
            <AccordionItemsDirective>
              <AccordionItemDirective header='Department' content='#content1' />
              <AccordionItemDirective header='Platform' content='#content2' />
              <AccordionItemDirective header='Employee Details' content= { this.props.data} />
            </AccordionItemsDirective>
        </AccordionComponent>
       );
  }
}
let ajax: Ajax = new Ajax('./ajax.html', 'GET', true);
ajax.send().then();
ajax.onSuccess = (dataSt: string): void => {
  ReactDOM.render(<ReactApp data={dataSt} />, document.getElementById("element") as HTMLElement); }

```

{% endtab %}