---
title: "Disable editing for a particular row/cell"
component: "Grid"
description: "Learn how to Disable editing for a particular row/cell."
---

# Disable editing for a particular row/cell

You can disable the editing for a particular row by using the [`actionBegin`](../../api/grid/#actionbegin) event of Grid based on **requestType** as **beginEdit**.

In the below demo, the rows which are having the value for *ShipCountry* column as *France* is prevented from editing.

{% tab template="grid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { DialogEditEventArgs, Edit, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true };
  public toolbarOptions: ToolbarItems[] = ['Edit', 'Update', 'Cancel'];

  public actionBegin(args: DialogEditEventArgs): void {
    if (args.requestType === 'beginEdit') {
      if ( getValue('ShipCountry', args.rowData as object) === "France") {
          args.cancel = true;
      }
    }
  }

  public render() {
    this.actionBegin = this.actionBegin.bind(this);
    return <GridComponent dataSource={data} actionBegin={this.actionBegin}
      editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
      <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
      </ColumnsDirective>
      <Inject services={[Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}

For batch mode of editing, you can use [`cellEdit`](../../api/grid/#celledit) event of Grid. In the below demo, the cells which are having the value as *France* is prevented from editing.

{% tab template="grid/customizedialog", sourceFiles="app/App.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { BatchAddArgs, Edit, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true, mode: 'Batch' };
  public toolbarOptions: ToolbarItems[] = ['Edit', 'Update', 'Cancel'];

  public cellEdit(args: BatchAddArgs): void {
    if (getValue('value', args) === "France") {
        args.cancel = true;
    }
  }

  public render() {
    this.cellEdit = this.cellEdit.bind(this);
    return <GridComponent dataSource={data} cellEdit={this.cellEdit}
      editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
      <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
      </ColumnsDirective>
      <Inject services={[Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}
