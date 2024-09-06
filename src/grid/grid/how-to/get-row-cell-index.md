---
title: "Get specific row and cell index in Grid"
component: "Grid"
description: "Learn how to get specific row and cell index in Grid."
---

# Get specific row and cell index in Grid

You can get the specific row and cell index of the grid by using [`rowSelected`](../../api/grid/#rowselected) event of the grid. Here, we can get the row and cell index by using *aria-rowindex* (get row Index from *tr* element) and *aria-colindex* (column index from *td* element) attribute.

 {% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, RowSelectEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public rowSelected(args: RowSelectEventArgs):void {
      alert("row index: "+(args.row as HTMLTableRowElement).getAttribute('aria-rowindex'));
      alert("column index: "+(args.target as HTMLElement).getAttribute('aria-colindex'));
  }

  public render(){
    this.rowSelected = this.rowSelected.bind(this);
    return <GridComponent  dataSource={data} rowSelected={this.rowSelected} height={267}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
        <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
        <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
      </ColumnsDirective>
    </GridComponent >
    }
};
```

{% endtab %}