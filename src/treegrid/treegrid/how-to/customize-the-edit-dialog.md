---
title: "Customize the Edit Dialog"
component: "TreeGrid"
description: "Learn how to customize the Edit Dialog."
---

# Customize the Edit Dialog

You can customize the appearance of the edit dialog in the [`actionComplete`](../api/treegrid/#actioncomplete) event based on **requestType** as **beginEdit** or **add**.

In the below example, we have changed the dialog's header text for editing and adding records.

{% tab template="treegrid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { getValue } from '@syncfusion/ej2-base';
import { Dialog } from '@syncfusion/ej2-popups';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { DialogEditEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];

  public actionComplete(args: DialogEditEventArgs): void {
    if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
      const dialog: Dialog = args.dialog as Dialog;
      dialog.height = 400;
      // change the header of the dialog
      dialog.header = args.requestType === 'beginEdit' ?
        'Record of ' +  getValue('TaskName', args.rowData) : 'New Customer';
    }
  }

  public render() {
    this.actionComplete = this.actionComplete.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' actionComplete={this.actionComplete} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar]} />
      </TreeGridComponent>
    );
  }
};

```

{% endtab %}