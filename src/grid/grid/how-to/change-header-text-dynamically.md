---
title: "Change Change Column Header Text Dynamically"
component: "Grid"
description: "Learn how to change column header text dynamically."
---

# Change Column Header Text Dynamically

You can change the column [`headerText`](../../api/grid/column/#headertext) dynamically through an external button.

Follow the given steps to change the header text dynamically:

**Step 1**:

Get the column object corresponding to the field name by using the [`getColumnByField`](../../api/grid/#getcolumnbyfield) method.
Then change the header Text value.

```typescript
      /** get the JSON object of the column corresponding to the field name */
      const column = this.grid.getColumnByField("ShipCity");
      /** assign a new header text to the column */
      column.headerText = "Changed Text";

```

**Step 2**:

To reflect the changes in the grid header, invoke the [`refreshHeader`](../../api/grid/#refreshheader) method.

```typescript

      this.grid.refreshHeader();

```

{% tab template="grid/change-headertext", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  private grid: Grid | null;

  public click() {
    if (this.grid) {
      /** get the JSON object of the column corresponding to the field name */
      const column = this.grid.getColumnByField("ShipCity");
      /** assign a new header text to the column */
      column.headerText = "Changed Text";
      this.grid.refreshHeader();
    }
  }
  public render() {
    this.click = this.click.bind(this);
    return (<div>
      <ButtonComponent cssClass= 'e-flat' onClick= { this.click }>Change Header Text</ButtonComponent>
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