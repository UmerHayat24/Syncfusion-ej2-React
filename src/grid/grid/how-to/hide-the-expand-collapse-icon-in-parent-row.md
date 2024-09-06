---
title: "Hide the expand/collapse icon in parent row with no record in child grid"
component: "Grid"
description: "Learn how to Hide the expand/collapse icon in parent row with no record in child grid."
---

# Hide the expand/collapse icon in parent row with no record in child grid

By default, the expand/collapse icon will be visible even if the child grid is empty.

You can use [`rowDataBound`](../../api/grid/#rowdatabound) event to hide the icon when there is no record in child grid.

To hide the expand/collapse icon in parent row with no record in child grid, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .e-row[aria-selected="true"] .e-customizedExpandcell {
        background-color: #e0e0e0;
    }

    .e-grid.e-gridhover tr[role='row']:hover {
        background-color: #eee;
    }

```

**Step 2**:

Add the CSS class to the Grid in the [`rowDataBound`](../../api/grid/#rowdatabound) event handler of Grid.

```typescript
   public rowDataBound(args:any): void{
    if (this.grid) {
      const filter:string = args.data.EmployeeID;
      const childrecord: object[] = new DataManager(this.grid.childGrid.dataSource as object[])
        .executeLocal(new Query().where("EmployeeID", "equal", parseInt(filter, 0), true));
      if(childrecord.length === 0) {
        // here hide which parent row has no child records
        args.row.querySelector('td').innerHTML=" ";
        args.row.querySelector('td').className = "e-customizedExpandcell";
      }
    }
  }

```

In the below demo, the expand/collapse icon in the row with *EmployeeID* as *1* is hidden as it does not have record in child Grid.

{% tab template="grid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { DetailRow, Grid, GridModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public dataManger: object = [{Order:100, ShipName:'Berlin', EmployeeID:2},
  {Order:101, ShipName:'Capte', EmployeeID:3},
  {Order:102, ShipName:'Marlon', EmployeeID:4},
  {Order:103, ShipName:'Black pearl', EmployeeID:5},
  {Order:104, ShipName:'Pearl', EmployeeID:6},
  {Order:105, ShipName:'Noth bay', EmployeeID:7},
  {Order:106, ShipName:'baratna', EmployeeID:8},
  {Order:107, ShipName:'Charge', EmployeeID:9}];
  public childGrid : GridModel = {
    columns: [
      { field: 'Order', headerText: 'Order ID', textAlign: 'Right', width: 120 },
      { field: 'EmployeeID', headerText: 'EmployeeID', width: 150 },
      { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: this.dataManger,
    queryString: 'EmployeeID'
  };
  public rowDataBound(args:any): void{
    if (this.grid) {
      const filter:string = args.data.EmployeeID;
      const childrecord: object[] = new DataManager(this.grid.childGrid.dataSource as object[])
        .executeLocal(new Query().where("EmployeeID", "equal", parseInt(filter, 0), true));
      if(childrecord.length === 0) {
        // here hide which parent row has no child records
        args.row.querySelector('td').innerHTML=" ";
        args.row.querySelector('td').className = "e-customizedExpandcell";
      }
    }
  }

  public render() {
    this.rowDataBound = this.rowDataBound.bind(this);
    return <GridComponent dataSource={data} childGrid={this.childGrid}
      rowDataBound={this.rowDataBound} ref={(scope) => { this.grid = scope; }}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
        <ColumnDirective field='CustomerID' width='100'/>
        <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
        <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
        <ColumnDirective field='ShipCountry' width='100'/>
      </ColumnsDirective>
      <Inject services={[DetailRow]}/>
    </GridComponent>
  }
};
```

{% endtab %}
