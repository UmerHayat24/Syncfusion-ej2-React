---
title: "Refresh the Datasource"
component: "Grid"
description: "Learn how to refresh the Grid dataSource."
---

# Refresh the data source

You can add/delete the datasource records through an external button. To reflect the datasource changes in grid,
you need to invoke the [`refresh`](../../api/grid/#refresh) method.

Please follow the below steps to refresh the grid after datasource change.

**Step 1**:

Add/delete the datasource record by using the following code.

```typescript
    /** Add a new record */
    this.grid.dataSource.unshift(data);

    /** Delete a record */
    this.grid.dataSource.splice(selectedRow, 1);

```

**Step 2**:

Refresh the grid after the datasource change by using the [`refresh`](../../api/grid/#refresh) method.

```typescript

    /** Refresh the Grid */
    this.grid.refresh();

```

{% tab template="grid/editing", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  private grid: Grid | null;
  public add() {
    if (this.grid) {
      const rec: object = { OrderID: 10247, CustomerID: "ASDFG", ShipCity: 'Vins et alcools Chevalier' , ShipName: 'Reims' };
      /** Add record */
      (this.grid.dataSource as object[]).unshift(rec);
      /** Refresh the Grid */
      this.grid.refresh();
    }
  }
  public delete() {
    if (this.grid) {
      const selectedRow: number = this.grid.getSelectedRowIndexes()[0];
      if (this.grid.getSelectedRowIndexes().length){
        /** Delete record */
        (this.grid.dataSource as object[]).splice(selectedRow, 1);
      }
      else {
          alert("No records selected for delete operation");
      }
      /** Refresh the Grid */
      this.grid.refresh();
    }
  }
  public render() {
    this.add = this.add.bind(this);
    this.delete = this.delete.bind(this);
    return (<div>
      <ButtonComponent cssClass= 'e-flat' onClick= { this.add }>Add</ButtonComponent>
      <ButtonComponent cssClass= 'e-flat' onClick= { this.delete }>Delete</ButtonComponent>
      <GridComponent dataSource={data} height={280} ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
          <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
        </ColumnsDirective>
      </GridComponent>
    </div>)
  }
};
```

{% endtab %}
