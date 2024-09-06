---
title: "Example of React Data Grid to show or hide columns in Dialog editing"
component: "Grid"
description: "Learn how to show or hide columns in Dialog editing with an example of React Data Grid."
---

# Example of React Data Grid to show or hide columns in Dialog editing

You can show hidden columns or hide visible column's editor in the dialog while editing the grid record using [`actionBegin`](../../api/grid/#actionbegin) and [`actionComplete`](../../api/grid/#actioncomplete) events.

In the [`actionBegin`](../../api/grid/#actionbegin) event, based on [`requestType`](../../api/grid/dialogEditEventArgs/#requesttype) as **beginEdit** or  **add**. We can show or hide the editor by using [`column.visible`](../../api/grid/column/#visible) property.

In the [`actionComplete`](../../api/grid/#actioncomplete) event, based on [`requestType`](../../api/grid/dialogEditEventArgs/#requesttype) as **save**. We can reset the properties back to the column state.

In the below example, we have rendered the grid columns *CustomerID* as hidden column and *ShipCountry* as visible column. In the edit mode, we have changed the *CustomerID* column to visible state and *ShipCountry* column to hidden state.

{% tab template="grid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Column, DialogEditEventArgs, Edit, Grid, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  private grid: Grid | null;

  public actionBegin(args: DialogEditEventArgs): void {
    if (this.grid && (args.requestType === 'beginEdit' || args.requestType === 'add')) {
      const cols: Column[] = this.grid.columns as Column[];
      for (const col of cols) {
        if (col.field === "CustomerID") {
          col.visible = true;
        }
        else if (col.field === "ShipCountry") {
          col.visible = false;
        }
      }
    }
  }
  public actionComplete(args: DialogEditEventArgs): void {
    if (this.grid && args.requestType === 'save') {
      const cols: Column[] = this.grid.columns as Column[];
      for (const col of cols) {
        if (col.field === "CustomerID") {
          col.visible = false;
        }
        else if (col.field === "ShipCountry") {
          col.visible = true;
        }
      }
    }
  }

  public render() {
    this.actionBegin = this.actionBegin.bind(this);
    this.actionComplete = this.actionComplete.bind(this);
    return <GridComponent dataSource={data} actionBegin={this.actionBegin}
      actionComplete={this.actionComplete} editSettings={this.editOptions}
      toolbar={this.toolbarOptions} height={265} ref={g => this.grid = g}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='120' visible={false}/>
        <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2' editType='numericedit'/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
      </ColumnsDirective>
      <Inject services={[Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}
