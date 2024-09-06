---
title: "Clipboard"
component: "Grid"
description: "Learn how to use the copy to clipboard functionality in the Essential JS 2 DataGrid Control."
---

# Clipboard

The clipboard provides an option to copy selected rows or cells data into the clipboard.

The following list of keyboard shortcuts is supported in the Grid to copy selected rows or cells data into clipboard.

Interaction keys |Description
-----|-----
<kbd>Ctrl + C</kbd> |Copy selected rows or cells data into clipboard.
<kbd>Ctrl + Shift + H</kbd> |Copy selected rows or cells data with header into clipboard.

{% tab template="grid/clipboard", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public settings: SelectionSettingsModel = { type: 'Multiple' };
  public render(){
    return <GridComponent  dataSource={data} selectionSettings={this.settings} height={272}>
            <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
              <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
              <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
            </ColumnsDirective>
          </GridComponent >
  }
}
```

{% endtab %}

## Copy to clipboard by external buttons

To copy selected rows or cells data into clipboard with help of external buttons, you need to invoke the [`copy`](../api/grid/clipboard/#copy)
method.

{% tab template="grid/clipboard", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  
  public grid: Grid | null;
  public settings: SelectionSettingsModel = { type: 'Multiple' };
  public copy(){
    if (this.grid) {
      this.grid.copy();
    }
  }
  
  public copyHeader(){
    if (this.grid) {
      this.grid.copy(true);
    }
  }
  
  public render() {
    this.copy = this.copy.bind(this);
    this.copyHeader = this.copyHeader.bind(this);
    return (<div>
      <ButtonComponent onClick= { this.copy }>Copy</ButtonComponent>
      <ButtonComponent onClick= { this.copyHeader }>CopyHeader</ButtonComponent>
      <GridComponent  dataSource={employeeData} height={280} ref={g => this.grid = g}
        selectionSettings={this.settings}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
          <ColumnDirective field='Country' headerText='Country' width='150'/>
        </ColumnsDirective>
      </GridComponent>
    </div>)
    }
}
```

{% endtab %}

## AutoFill

AutoFill Feature allows you to copy the data of selected cells and paste it to another cells by just dragging the autofill icon of the selected cells up to required cells. This feature is enabled by defining [`enableAutoFill`](../api/grid/#enableautofill) property as **true**.

{% tab template="grid/clipboard", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import { Edit, EditSettingsModel, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' };
  public settings: SelectionSettingsModel = { cellSelectionMode: 'Box', type: 'Multiple', mode: 'Cell' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Update', 'Cancel'];
  public render(){
    return <GridComponent  dataSource={data} toolbar={this.toolbarOptions}
              editSettings={this.editOptions} selectionSettings={this.settings}
              enableAutoFill={true} height={272}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right" isPrimaryKey={true} visible={false}/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipCountry' headerText='ShipCountry' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Edit, Toolbar]} />
            </GridComponent >
    }
}
```

{% endtab %}

> * If [`enableAutoFill`](../api/grid/#enableautofill) is set to **true**, then the autofill icon will be displayed on cell selection to copy cells.
> * It requires the selection [`mode`](../api/grid/selectionSettingsModel/#mode) to be **Cell**,  [`cellSelectionMode`](../api/grid/selectionSettingsModel/#cellselectionmode) to be **Box** and also Batch Editing should be enabled.

### Limitations of AutoFill

* Since the string values are not parsed to number and date type, so when the selected string type cells are dragged to number type cells then it will display as **NaN**. For date type cells, when the selected string type cells are dragged to date type cells then it will display as an **empty cell**.
* Linear series and the sequential data generations are not supported in this autofill feature.

## Paste

You can able to copy the content of a cell or a group of cells by selecting the cells and pressing <kbd>Ctrl + C</kbd> shortcut key and paste it to another set of cells by selecting the cells and pressing <kbd>Ctrl + V</kbd> shortcut key.

{% tab template="grid/clipboard", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import { Edit, EditSettingsModel, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' };
  public settings: SelectionSettingsModel = { cellSelectionMode: 'Box', type: 'Multiple', mode: 'Cell' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Update', 'Cancel'];
  public render(){
    return <GridComponent  dataSource={data} toolbar={this.toolbarOptions}
              editSettings={this.editOptions} selectionSettings={this.settings}
              enableAutoFill={true} height={272}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right" isPrimaryKey={true} visible={false}/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipCountry' headerText='ShipCountry' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Edit, Toolbar]} />
            </GridComponent >
    }
}
```

{% endtab %}

> To perform paste functionality, it requires the selection **mode** to be **Cell**,  [`cellSelectionMode`](../api/grid/selectionSettingsModel/#cellselectionmode) to be **Box** and also Batch Editing should be enabled.

### Limitations of Paste Functionality

Since the string values are not parsed to number and date type, so when the copied string type cells are pasted to number type cells then it will display as **NaN**. For date type cells, when the copied string format cells are pasted to date type cells then it will display as an **empty cell**.