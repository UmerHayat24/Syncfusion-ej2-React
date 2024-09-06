---
title: "Context Menu"
component: "Grid"
description: "Learn how to use the context menu and add custom context menu items in the Essential JS 2 DataGrid control."
---

# Context menu

The Grid has options to show the context menu when right clicked on it.
To enable this feature, you need to define either default or custom item in the [`contextMenuItems`](../api/grid/#contextmenuitems).

To use the context menu, inject the **ContextMenu** module in the grid.

The default items are in the following table.

Items| Description
----|----
`AutoFit`|  Auto fit the current column.
`AutoFitAll` | Auto fit all columns.
`Edit`|  Edit the current record.
`Delete` | Delete the current record.
`Save` | Save the edited record.
`Cancel` | Cancel the edited state.
`Copy` | Copy the selected records.
`PdfExport` | Export the grid data as Pdf document.
`ExcelExport` | Export the grid data as Excel document.
`CsvExport` | Export the grid data as CSV document.
`Group` | Group the current column.
`Ungroup` | Ungroup the current column.
`SortAscending` | Sort the current column in ascending order.
`SortDescending` | Sort the current column in descending order.
`FirstPage` | Go to the first page.
`PrevPage` | Go to the previous page.
`LastPage` | Go to the last page.
`NextPage` | Go to the next page.

{% tab template="grid/clipboard", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, GroupSettingsModel } from '@syncfusion/ej2-react-grids';
import { ContextMenu, Edit, EditSettingsModel, Filter, Group, Inject, Page, Sort } from '@syncfusion/ej2-react-grids';
import { ContextMenuItem, ExcelExport, PdfExport } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public groupOptions: GroupSettingsModel = { showGroupedColumn: true };
  public contextMenuItems: ContextMenuItem[] = ['AutoFit', 'AutoFitAll',
      'SortAscending', 'SortDescending', 'Copy', 'Edit', 'Delete', 'Save',
      'Cancel', 'PdfExport', 'ExcelExport', 'CsvExport', 'FirstPage', 'PrevPage',
      'LastPage', 'NextPage'];
  public editing: EditSettingsModel = { allowDeleting: true, allowEditing: true };

  public render() {
    return (
      <div>
          <GridComponent dataSource={data} allowPaging={true} allowSorting={true}
              allowExcelExport={true} allowPdfExport={true} contextMenuItems={this.contextMenuItems}
              editSettings={this.editing} allowGrouping={true} groupSettings={this.groupOptions}>
              <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign='Right' isPrimaryKey={true}/>
                  <ColumnDirective field='CustomerID' headerText='Customer Name' width='140'/>
                  <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' editType='numericedit' width='140' />
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='200'/>
              </ColumnsDirective>
              <Inject services={[Sort, ContextMenu, Filter, Page, ExcelExport, Edit, PdfExport, Group]} />
          </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

## Custom context menu items

The custom context menu items can be added by defining the [`contextMenuItems`](../api/grid/#contextmenuitems) as a collection of [`contextMenuItemModel`](../api/grid/contextMenuItemModel).
Actions for this customized items can be defined in the [`contextMenuClick`](../api/grid/#contextmenuclick) event.

{% tab template="grid/clipboard", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { MenuEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { ContextMenu, ContextMenuItemModel, Inject, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public contextMenuItems: ContextMenuItemModel[] = [
    {text: 'Copy with headers', target: '.e-content', id: 'copywithheader'}
  ];

  public contextMenuClick(args: MenuEventArgs){
      if(this.grid && args.item.id === 'copywithheader'){
          this.grid.copy(true);
      }
  }

  public render() {
    this.contextMenuClick = this.contextMenuClick.bind(this);
    return (
      <div>
        <GridComponent dataSource={data} allowPaging={true} contextMenuItems={this.contextMenuItems}
          ref={g=> this.grid = g} contextMenuClick={this.contextMenuClick}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign='Right'/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='140'/>
              <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' width='140' />
              <ColumnDirective field='ShipName' headerText='Ship Name' width='200'/>
          </ColumnsDirective>
          <Inject services={[ContextMenu, Page]} />
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

> You can hide or show an item in context menu for specific area inside of grid by defining the
[`target`](../api/grid/contextMenuItemModel/#target) property.

## See also

* [How can I dynamically enable/disable a ContextMenu item inside a React Grid](https://www.syncfusion.com/forums/159508/how-can-i-dynamically-enable-disable-a-contextmenu-item-inside-a-react-grid)
