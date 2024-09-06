---
title: "Customize Pager DropDown"
component: "Grid"
description: "Learn how to Customize Pager DropDown."
---

# Customize Pager DropDown

To customize default values of pager dropdown, you need to define [`pageSizes`](../../api/grid/pageSettings/#pagesizes) as array of strings.

{% tab template="grid/pager", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public pageOptions: PageSettingsModel = {pageSizes: ["5", "10", "All"]};
  public render() {
    return <GridComponent dataSource={data} allowPaging={true} pageSettings={this.pageOptions} height={273}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
        <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
      </ColumnsDirective>
      <Inject services={[Page]} />
    </GridComponent>
  }
};
```

{% endtab %}
