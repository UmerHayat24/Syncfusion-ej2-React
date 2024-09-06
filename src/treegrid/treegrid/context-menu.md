---
title: "Context Menu"
component: "TreeGrid"
description: "Learn how to use the context menu and add custom context menu items in the Essential JS 2 TreeGrid control."
---

# Context menu

The TreeGrid has options to show the context menu when right clicked on it. To enable this feature, you need to define either default or custom item in the [`contextMenuItems`](../api/treegrid/#contextmenuitems).

To use the context menu, inject the **ContextMenu** module in the treegrid.

The default items are in the following table.

Items| Description
----|----
**AutoFit**|  Auto fit the current column.
**AutoFitAll** | Auto fit all columns.
**Edit**|  Edit the current record.
**Delete** | Delete the current record.
**Save** | Save the edited record.
**Cancel** | Cancel the edited state.
**PdfExport** | Export the treegrid data as Pdf document.
**ExcelExport** | Export the treegrid data as Excel document.
**CsvExport** | Export the treegrid data as CSV document.
**SortAscending** | Sort the current column in ascending order.
**SortDescending** | Sort the current column in descending order.
**FirstPage** | Go to the first page.
**PrevPage** | Go to the previous page.
**LastPage** | Go to the last page.
**NextPage** | Go to the next page.
**AddRow** | Add new row to the treegrid.

{% tab template="treegrid/contextmenu", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, Page, Resize, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ContextMenu, ContextMenuItem, Edit, ExcelExport, Inject, PdfExport, Sort } from '@syncfusion/ej2-react-treegrid';
import { EditSettingsModel, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editSettings: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Row'
    };
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public contextMenuItems: ContextMenuItem[] = ['AutoFit', 'AutoFitAll',
        'SortAscending', 'SortDescending', 'Edit', 'Delete', 'Save',
        'Cancel', 'PdfExport', 'ExcelExport', 'CsvExport', 'FirstPage', 'PrevPage',
        'LastPage', 'NextPage'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowSorting='true' allowResizing='true'
        editSettings={this.editSettings} allowPdfExport='true' allowExcelExport='true'
        contextMenuItems={this.contextMenuItems}>
            <ColumnsDirective>
                <ColumnDirective field='taskID' isPrimaryKey={true} headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Resize, Sort, Edit, ContextMenu, Page, PdfExport, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Custom context menu items

The custom context menu items can be added by defining the [`contextMenuItems`](../api/treegrid/#contextmenuitems) as a collection of [`contextMenuItemModel`](../api/grid/contextMenuItemModel/).
Actions for this customized items can be defined in the [`contextMenuClick`](../api/treegrid/#contextmenuclick) event.

In the below sample, we have shown context menu item for parent rows to expand or collapse child rows.

{% tab template="treegrid/contextmenu", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getValue, isNullOrUndefined } from '@syncfusion/ej2-base';
import { ContextMenuItemModel } from '@syncfusion/ej2-grids';
import { BeforeOpenCloseMenuEventArgs, MenuEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ContextMenu,  Inject, PageSettingsModel, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public contextMenuItems: ContextMenuItemModel[] = [
        {text: 'Collapse the Row', target: '.e-content', id: 'collapserow'},
        {text: 'Expand the Row', target: '.e-content', id: 'expandrow'}
    ];
    public contextMenuClick(args: MenuEventArgs): void {
        if (this.treegrid) {
            this.treegrid.getColumnByField('taskID');
            if (args.item.id === 'collapserow') {
                this.treegrid.collapseRow(this.treegrid.getSelectedRows()[0] as HTMLTableRowElement,
                    this.treegrid.getSelectedRecords()[0]);
            } else {
                this.treegrid.expandRow(this.treegrid.getSelectedRows()[0] as HTMLTableRowElement,
                    this.treegrid.getSelectedRecords()[0]);
            }
        }
    }

    public contextMenuOpen(args: BeforeOpenCloseMenuEventArgs): void {
        const elem: HTMLElement = args.event.target as HTMLElement;
        const uid: string = (elem.closest('.e-row') as HTMLElement).getAttribute('data-uid') as string;
        if (this.treegrid) {
            if (isNullOrUndefined(getValue('hasChildRecords',
                this.treegrid.grid.getRowObjectFromUID(uid) .data))) {
                args.cancel = true;
            } else {
                const flag: boolean = getValue('expanded', this.treegrid.grid.getRowObjectFromUID(uid).data);
                let val: string = flag ? 'none' : 'block';
                document.querySelectorAll('li#expandrow')[0].setAttribute('style', 'display: ' + val + ';');
                val = !flag ? 'none' : 'block';
                document.querySelectorAll('li#collapserow')[0].setAttribute('style', 'display: ' + val + ';');
            }
        }
    }


    public render() {
        this.contextMenuClick = this.contextMenuClick.bind(this);
        this.contextMenuOpen = this.contextMenuOpen.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
        allowPaging='true' pageSettings={this.pageSettings} allowSorting='true' allowResizing='true'
        contextMenuItems={this.contextMenuItems} contextMenuClick={this.contextMenuClick}
        ref={treegrid=> this.treegrid = treegrid} contextMenuOpen={this.contextMenuOpen}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[ContextMenu, Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> You can hide or show an item in context menu for specific area inside of treegrid by defining the [`target`](../api/grid/contextMenuItemModel/#target) property.