---
title: "Perform Grid actions by keyboard shortcut keys"
component: "Grid"
description: "Learn how to Perform Grid actions by keyboard shortcut keys."
---

# Perform Grid actions by keyboard shortcut keys

Using keyboard shortcuts, Grid performs navigation and actions.

In addition, You can also perform grid actions with custom keyboard shortcuts. This operation has to be achieved outside of the grid with the help of **keydown** event.

The following example demonstrates on *Adding* a new row when **Enter** key is pressed in the grid.

{% tab template="grid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Edit, Grid, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Normal' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  private grid: Grid | null;

  public load(): void {
    if (this.grid) {
      this.grid.element.addEventListener('keydown', this.keyDownHandler);
    }
  }

  public keyDownHandler(e: any): void {
    if (this.grid && e.keyCode === 13) {
      this.grid.addRecord();
    }
  }

  public render() {
    this.load = this.load.bind(this);
    this.keyDownHandler = this.keyDownHandler.bind(this);
    return <GridComponent dataSource={data} load={this.load}
    editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}
      ref={g => this.grid = g}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
        <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2' editType='numericedit'/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
      </ColumnsDirective>
      <Inject services={[Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}
