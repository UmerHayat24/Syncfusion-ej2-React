---
title: "Enable editing in single click"
component: "Grid"
description: "Learn how to enable single click editing in the Essential JS 2 DataGrid control."
---

# Enable editing in single click

## Normal Editing

You can make a row editable on a single click with **Normal** mode of editing in Grid, by using the [`startEdit`](../../api/grid/#startedit) and [`endEdit`](../../api/grid/#endedit) methods.

Bind the **mouseup** event for Grid and in the event handler call the [`startEdit`](../../api/grid/#startedit) and [`endEdit`](../../api/grid/#endedit), based on the clicked target element.

{% tab template="grid/editing", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Edit, Page, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-grids';
import { MouseEventArgs } from '@syncfusion/ej2-base';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
    public editSettings: EditSettingsModel = { allowEditing: true, allowAdding:   true, allowDeleting: true, mode: 'Normal' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public load(): void {
        let instance = this.gridInstance;
        instance.element.addEventListener('mouseup', function (e) {
            if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
                if (instance.isEdit)
                    instance.endEdit();
                let index: number = parseInt((e.target as HTMLElement).getAttribute("Index"));
                instance.selectRow(index);
                instance.startEdit();
            };
        });
    }
    public render() {
      return <GridComponent dataSource={data} ref={grid => this.gridInstance = grid} toolbar={this.toolbarOptions} allowPaging={true} editSettings={this.editSettings} load={this.load.bind(this)}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' textAlign='Right' width='100' isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' textAlign='Right'  width='120' format='C2' ></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
              </ColumnsDirective>
              <Inject services={[Page, Toolbar, Edit]}/>
            </GridComponent>
    }
}
```

{% endtab %}

### Open dropdown edit popup on single click

You can open the default dropdown edit popup with single click edit by focusing the dropdown element and calling the EJ2 dropdown list's [`showPopup`](../../api/drop-down-list/#showpopup) method in the Grid's [`actionComplete`](../../api/grid/#actioncomplete) event. In this demo we have used a global flag variable in the **mouseup** event to ensure if the dropdown column is the clicked edit target.

{% tab template="grid/editing", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Edit, Page, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-grids';
import { MouseEventArgs } from '@syncfusion/ej2-base';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
    public editSettings: EditSettingsModel = { allowEditing: true, allowAdding:   true, allowDeleting: true, mode: 'Normal' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public isDropdown = false;

    public load(): void {
        this.gridInstance.element.addEventListener('mouseup', function (e) {
            if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
              if (this.gridInstance.isEdit)
                  this.gridInstance.endEdit();
              let rowInfo = this.gridInstance.getRowInfo(e.target);
              if (rowInfo.column.field === "ShipCountry")
                  this.isDropdown = true;
              this.gridInstance.selectRow(rowInfo.rowIndex);
              this.gridInstance.startEdit();
            };
        }.bind(this));
    }

    public onActionComplete(args) {
        if (args.requestType =="beginEdit" && this.isDropdown) {
            this.isDropdown = false;
            let dropdownObj = args.form.querySelector('.e-dropdownlist').ej2_instances[0];
            dropdownObj.element.focus();
            dropdownObj.showPopup();
        }
    }

    public render() {
      return <GridComponent dataSource={data} ref={grid => this.gridInstance = grid} toolbar={this.toolbarOptions} allowPaging={true} editSettings={this.editSettings} load={this.load.bind(this)} actionComplete={this.onActionComplete.bind(this)}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' textAlign='Right' width='100' isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' textAlign='Right'  width='120' format='C2' ></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' editType='dropdownedit' width='150'></ColumnDirective>
              </ColumnsDirective>
              <Inject services={[Page, Toolbar, Edit]}/>
            </GridComponent>
    }
}
```

{% endtab %}

## Batch Editing

You can make a cell editable on a single click with **Batch** mode of editing in Grid, by using the [`editCell`](../../api/grid/edit/#editcell) method.

Bind the **mouseup** event for Grid and in the event handler call the [`editCell`](../../api/grid/edit/#editcell) method, based on the clicked target element.

{% tab template="grid/editing", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Edit, Page, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
    public editSettings: EditSettingsModel = { allowEditing: true, allowAdding:   true, allowDeleting: true, mode: 'Batch' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public load(): void {
        let instance = this.gridInstance;
        instance.element.addEventListener('mouseup', (e: MouseEventArgs) => {
        if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
            let index: number = parseInt((e.target as HTMLElement).parentElement.getAttribute("aria-rowindex"));
            let colindex: number = parseInt((e.target as HTMLElement).getAttribute("aria-colindex"));
            let field: string = instance.getColumns()[colindex].field;
            instance.editModule.editCell(index, field);
        };
        });
    }
    public render() {
      return <GridComponent dataSource={data} ref={grid => this.gridInstance = grid} toolbar={this.toolbarOptions} allowPaging={true} editSettings={this.editSettings} load={this.load.bind(this)}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' textAlign='Right' width='100' isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' textAlign='Right'  width='120' format='C2' ></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
              </ColumnsDirective>
              <Inject services={[Page, Toolbar, Edit]}/>
            </GridComponent>
    }
}
```

{% endtab %}