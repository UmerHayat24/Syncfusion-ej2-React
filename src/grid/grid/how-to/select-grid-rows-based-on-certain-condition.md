---
title: "Select grid rows based on certain condition"
component: "Grid"
description: "Learn how to select rows in grid based on certain condition"
---

# Select grid rows based on certain condition

You can select the specific row in the grid based on a certain condition by using the [`selectRows`](../../api/grid/#selectrows) method in the [`dataBound`](../../api/grid/#databound) event of Grid.

In the below demo, we have selected the grid rows only when *EmployeeID* column value greater than *3*.

{% tab template="grid/change-headertext", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Page } from '@syncfusion/ej2-react-grids';
import { Grid, RowDataBoundEventArgs, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public selIndex: number[] = [];
  public grid: Grid | null;
  public settings: SelectionSettingsModel = { type: 'Multiple' };
  public rowDataBound(args:RowDataBoundEventArgs):void {
    if (getValue('EmployeeID', args.data as object) > 3) {
      this.selIndex.push(parseInt((args.row as HTMLTableRowElement)
        .getAttribute('aria-rowindex') as string, 0));
    }
  }
  public dataBound():void {
    if (this.grid && this.selIndex.length) {
        this.grid.selectRows(this.selIndex);
        this.selIndex = [];
    }
  }
  public render() {
    this.rowDataBound = this.rowDataBound.bind(this);
    this.dataBound = this.dataBound.bind(this);
    return (<div>
      <GridComponent dataSource={data} allowPaging={true} rowDataBound={this.rowDataBound} dataBound={this.dataBound} selectionSettings={this.settings} height={280} ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='150' textAlign='Right'/>
          <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
        </ColumnsDirective>
        <Inject services={[Page]} />
      </GridComponent>
    </div>)
  }
};
```

{% endtab %}