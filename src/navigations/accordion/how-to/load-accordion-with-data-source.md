---
title: "Load accordion with DataSource"
component: "Accordion"
description: "This example demonstrates how to bind any data object to accordion items in the Essential JS 2 Accordion control."
---

# Load accordion with DataSource

You can bind any data object to Accordion items, by mapping it to
[`header`](../../api/accordion/accordionItem#header) and [`content`](../../api/accordion/accordionItem#content) property.

In the below demo, Data is fetched from an `OData` service using `DataManager`. The result data is
formatted as a JSON object with `header` and `content` fields, which is set to items property of Accordion.

{% tab template="accordion/accordion", compileJsx=true %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";
import { DataManager, Query, ODataV4Adaptor, ReturnOption } from '@syncfusion/ej2-data';
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-react-navigations';

const SERVICE_URI: string = 'https://services.odata.org/V4/Northwind/Northwind.svc/Employees';

class ReactApp extends React.Component<{}, {}> {
  public accordCreated(): void {
    new DataManager({ url: SERVICE_URI, adaptor: new ODataV4Adaptor})
    .executeQuery(new Query().range(1, 4)).then((e: ReturnOption) => {
      let itemsData: Object[] = [];
      let result: any = e.result;
      let mapping =  { header: 'FirstName', content: 'Notes' };
      for(let i: number = 0; i < result.length; i++) {
        itemsData.push({ header: result[i][mapping.header], content: result[i][mapping.content] });
      }
      this.items = itemsData;
      this.refresh();
    });
  }

  render() {
       return (
        <AccordionComponent ref={acrdn => this.acrdnInstance = acrdn} created={this.accordCreated}>
        </AccordionComponent>
      );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));

```

{% endtab %}
