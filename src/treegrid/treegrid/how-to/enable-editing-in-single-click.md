---
title: "Enable editing in single click"
component: "TreeGrid"
description: "Learn how to enable single click editing in the Essential JS 2 TreeGrid control."
---

# Enable editing in single click

## Row Editing

You can make a row editable on a single click with **Row** mode of editing in TreeGrid, by using the [`startEdit`](https://ej2.syncfusion.com/react/documentation/api/treegrid#startedit) and [`endEdit`](https://ej2.syncfusion.com/react/documentation/api/treegrid#endedit) methods.

Bind the **mousedown** event for TreeGrid and in the event handler call the [`startEdit`](https://ej2.syncfusion.com/react/documentation/api/treegrid#startedit) and [`endEdit`](https://ej2.syncfusion.com/react/documentation/api/treegrid#endedit), based on the clicked target element.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Page, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component<{}, {action: string}> {

  public treegrid: TreeGridComponent | null;
  public editSettings: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  public load(): void {
    let instance = this.treegrid as TreeGridComponent;
    instance.element.addEventListener('mousedown', function (e) {
        if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
            if (instance.grid.isEdit) {
              instance.endEdit();
            }
            let index: number = parseInt((e.target as HTMLElement).getAttribute('Index') as string);
            instance.selectRow(index);
            instance.startEdit();
        };
    });
  }
  public render() {
    this.load = this.load.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={210}
      allowPaging={true} toolbar={this.toolbarOptions} editSettings={this.editSettings} load={this.load.bind(this)}
      ref={g => this.treegrid = g}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='120'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Page, Edit, Toolbar]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}

## Cell Editing

You can make a cell editable on a single click with **Cell** mode of editing in TreeGrid, by using the [`editCell`](https://ej2.syncfusion.com/react/documentation/api/treegrid#editcell) method.

Bind the **mousedown** event for TreeGrid and in the event handler call the [`editCell`](https://ej2.syncfusion.com/react/documentation/api/treegrid#editcell) method, based on the clicked target element.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Page, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component<{}, {action: string}> {

  public treegrid: TreeGridComponent | null;
  public editSettings: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];
  public load(): void {
    let instance = this.treegrid as TreeGridComponent;
    instance.element.addEventListener('mousedown', function (e) {
        if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
          if (instance.grid.isEdit) {
            instance.grid.saveCell();
          }
          let index: number = parseInt((e.target as HTMLElement).getAttribute("Index") as string);
          let colindex: number = parseInt((e.target as HTMLElement).getAttribute("aria-colindex") as string);
          let field: string = instance.getColumns()[colindex].field;
          instance.editModule.editCell(index, field);
        };
    });
  }
  public render() {
    this.load = this.load.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={210}
      allowPaging={true} toolbar={this.toolbarOptions} editSettings={this.editSettings} load={this.load.bind(this)}
      ref={g => this.treegrid = g}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='120'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Page, Edit, Toolbar]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}