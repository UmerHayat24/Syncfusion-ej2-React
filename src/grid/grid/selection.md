---
title: "Selection"
component: "Grid"
description: "Learn how to select rows and cells, use range selection, and use check box selection in the Essential JS 2 DataGrid control."
---

# Selection

Selection provides an option to highlight a row or cell or column.
Selection can be done through simple Mouse down or Arrow keys.
To disable selection in the Grid, set the [`allowSelection`](../api/grid/#allowselection) to false.

The grid supports two types of selection that can be set by using the
[`selectionSettings.type`](../api/grid/selectionSettings/#type). They are:

* **Single** - The **Single** is set by default. Allows you to select only a single row or cell or column.
* **Multiple** - It allows you to select multiple rows or cells or columns.
To perform the multi-selection, press and hold CTRL key and click the desired rows or cells or columns.
To select range of rows or cells or columns, press and hold the SHIFT key and click the rows or cells or columns.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public settings: SelectionSettingsModel = { type: 'Multiple' };
  public render() {
      return <GridComponent dataSource={this.data} selectionSettings={this.settings} height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Selection Mode

The grid supports three types of selection mode that can be set by using
the [`selectionSettings.mode`](../api/grid/selectionSettings/#mode). They are:

* **Row** - The **Row** value is set by default. Allows you to select rows only.
* **Cell** - Allows you to select cells only.
* **Both** - Allows you to select rows and cells at the same time.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = { mode: 'Both' };
    public render() {
        return <GridComponent dataSource={data} selectionSettings={this.settings} height={315}>
                <ColumnsDirective>
                 <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                 <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                 <ColumnDirective field='ShipCity' headerText='Ship City' width='100'/>
                 <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
};
```

{% endtab %}

## Cell Selection

Cell Selection can be done through simple Mouse down or Arrow keys(up, down, left and right).

The grid supports two types of cell selection mode that can be set by using
the [`selectionSettings.cellSelectionMode`](../api/grid/selectionSettings/#cellselectionmode). They are:

* **Flow** - The **Flow** value is set by default.
Select range of cells between the start index and end index which includes in between cells of rows.
* **Box** - Select range of cells within the start and end column indexes which includes
in between cells of rows within the range.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public settings: SelectionSettingsModel = {
    cellSelectionMode: 'Box',
    mode: 'Cell',
    type: 'Multiple'
  };
  public render() {
      return <GridComponent dataSource={this.data} selectionSettings={this.settings} height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

> Cell Selection requires the [`selectionSettings.mode`](../api/grid/selectionSettings/#mode) to be **Cell** or  **Both** and
[`type`](../api/grid/selectionSettings/#type) should be **Multiple**.

## Column selection

Column selection can be done through simple mouse down or arrow keys.

You can enable column selection by setting the [`selectionSettings.allowColumnSelection`](../api/grid/selectionSettings/#allowcolumnselection) property as true.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public settings: SelectionSettingsModel = {
    allowColumnSelection: true,
    type: 'Multiple'
  };
  public render() {
      return <GridComponent dataSource={this.data} selectionSettings={this.settings} height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Checkbox selection

Checkbox selection provides an option to select multiple grid records with help of checkbox in each row.

To render the checkbox in each grid row, you need to use checkbox column with type as
**checkbox** using the  column [`type`](../api/grid/column/#type) property.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} height={315}>
            <ColumnsDirective>
             <ColumnDirective type='checkbox' width='50'/>
             <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
             <ColumnDirective field='CustomerID' width='150'/>
             <ColumnDirective field='ShipCity' width='100'/>
             <ColumnDirective field='ShipName' width='150'/>
            </ColumnsDirective>
           </GridComponent>
  }
};
```

{% endtab %}

> By default, selection is allowed by clicking a grid row or checkbox in that row. To allow selection only through checkbox,
you can set the
[`selectionSettings.checkboxOnly`](../api/grid/selectionSettings/#checkboxonly) property to true.
> Selection can be persisted in all the operations using the
[`selectionSettings.persistSelection`](../api/grid/selectionSettings/#persistselection) property.
For persisting selection on the grid, any one of the columns should be defined as a primary key using the
[`columns.isPrimaryKey`](../api/grid/column/#isprimarykey) property.

### Checkbox selection Mode

In checkbox selection, selection can also be done by clicking on rows. This selection provides two types of Checkbox Selection mode which can be set by using the following API, [`selectionSettings.checkboxMode`](../api/grid/selectionSettings/#checkboxmode). The modes are;

* **Default**: This is the default value of the checkboxMode. In this mode, user can select multiple rows by clicking rows one by one.
* **ResetOnRowClick**: In **ResetOnRowClick** mode, when user clicks on a row it will reset previously selected row. Also you can perform multiple-selection in this mode by press
and hold CTRL key and click the desired rows. To select range of rows, press and hold the SHIFT key and click the rows.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public settings: SelectionSettingsModel = { checkboxMode: 'ResetOnRowClick'};
  public render() {
      return <GridComponent dataSource={data} height={315} selectionSettings={this.settings}>
              <ColumnsDirective>
               <ColumnDirective type='checkbox' width='50'/>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Toggle selection

The Toggle selection allows to perform selection and unselection of the particular row or cell or column. To enable toggle selection, set [`enableToggle`](../api/grid/selectionSettings/#enabletoggle) property of the **selectionSettings** as **true**. If you click on the selected row or cell or column then it will be unselected and vice versa.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public settings: SelectionSettingsModel = { checkboxMode: 'ResetOnRowClick'};
  public render() {
      return <GridComponent dataSource={data} height={315} selectionSettings={this.settings}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

> If multi selection is enabled, then first click on any selected row (without pressing Ctrl key), it will clear the multi selection and in second click on the same row, it will be unselected.

## Select row at Initial rendering

To select a row at initial rendering, set the [`selectedRowIndex`](../api/grid/#selectedrowindex) value.

 {% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public settings: SelectionSettingsModel = { type: 'Multiple', mode: 'Both' };
  public render() {
      return <GridComponent dataSource={data} selectedRowIndex={1} selectionSettings={this.settings}
              height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Get Selected Row Indexes

You can get the selected row indexes by using the [`getSelectedRowIndexes`](../api/grid/#getselectedrowindexes) method.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public rowSelected() {
    if (this.grid) {
      /** Get the selected row indexes */
      const selectedrowindex: number[] = this.grid.getSelectedRowIndexes();
      /** Get the selected records. */
      const selectedrecords: object[] = this.grid.getSelectedRecords();
      alert(selectedrowindex + " : " + JSON.stringify(selectedrecords));
    }
  }
  public render() {
      this.rowSelected = this.rowSelected.bind(this);
      return <GridComponent dataSource={data} height={315} rowSelected={this.rowSelected}
              ref={g => this.grid = g}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Touch Interaction

When you tap a grid row on touchscreen device, the tapped row is selected.
It also shows a popup ![Selection](images/selection.jpg)  for multi-row selection.
To select multiple rows or cells, tap the popup![Multi Selection](images/mselection.jpg)  and then tap the desired rows or cells.

> For multi-selection, It requires the selection [`type`](../api/grid/selectionSettings/#type) to be **Multiple**.

The following screenshot represents a grid touch selection in the device.

![Touch Interaction](images/touch-selection.jpg)

> [`getSelectedRecords`](../api/grid/#getselectedrecords) method has been used to retrieve the selected records.

## Simple Multiple Row selection

You can select multiple rows by clicking on rows one by one. This will not deselect the previously selected rows. To deselect the previously selected row, you can click on the  selected row. You can enable this behavior by using [`selectionSettings.enableSimpleMultiRowSelection`](../api/grid/selectionSettings/#enablesimplemultirowselection) property.

{% tab template="grid/selection", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public settings: SelectionSettingsModel = {
    enableSimpleMultiRowSelection: true,
    type: 'Multiple'
  };
  public render() {
      return <GridComponent dataSource={data} selectionSettings={this.settings} height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='120' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='150'/>
               <ColumnDirective field='ShipCity' width='100'/>
               <ColumnDirective field='ShipName' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## See Also

* [How to select row at initial rendering by record ID in React Grid](https://www.syncfusion.com/forums/152812/how-to-select-row-at-initial-rendering-by-record-id-in-react-grid)
* [How to update the row while deselecting by using keyboard down arrow in React Grid](https://www.syncfusion.com/forums/152287/how-to-update-the-row-while-deselecting-by-using-keyboard-down-arrow-in-react-grid)