---
title: "Load tab with DataSource"
component: "Tab"
description: "This example demonstrates how to bind any data object to tab Items in the Essential JS 2 Tab control."
---

# Load tab with DataSource

You can bind any data object to Tab items, by mapping it to a
[`header`](../../api/tab/tabItem#header) and [`content`](../../api/tab/tabItem#content) property.

In the below demo, Data is fetched from an `OData` service using `DataManager`. The result data is formatted as
a JSON object with `header` and `content` fields, which is set to [`items`](../../api/accordion#items) property of Tab.

{% tab template="tab/tab", isDefaultActive=true, compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { DataManager, Query, ODataV4Adaptor, ReturnOption } from '@syncfusion/ej2-data';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';

const SERVICE_URI: string = 'https://services.odata.org/V4/Northwind/Northwind.svc/Employees';

export default class App extends React.Component<{}, {}> {

  public tabCreated(): void {
    new DataManager({ url: SERVICE_URI, adaptor: new ODataV4Adaptor})
    .executeQuery(new Query().range(1, 4)).then((e: ReturnOption) => {
      let itemsData: Object[] = [];
      let result: any = e.result;
      let mapping =  { header: 'FirstName', content: 'Notes' };
      for(let i: number = 0; i < result.length; i++) {
        itemsData.push({ header: { text: result[i][mapping.header] }, content: result[i][mapping.content] });
      }
      this.items = itemsData;
      this.refresh();
    });
  }

  render() {
    return (
      <TabComponent heightAdjustMode='Auto' ref={tab => this.tabInstance = tab} created={this.tabCreated}>
      </TabComponent>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
