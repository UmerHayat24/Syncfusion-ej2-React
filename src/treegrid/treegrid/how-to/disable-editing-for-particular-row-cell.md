---
title: "Disable editing for a particular row/cell"
component: "TreeGrid"
description: "Learn how to Disable editing for a particular row/cell."
---

# Disable editing for a particular row/cell

You can disable the editing for a particular row by using the [`actionBegin`](../api/treegrid/#actionbegin) event of Grid based on **requestType** as **beginEdit**.

In the below demo, the rows which are having the value for *Priority* column as *Breaker* is prevented from editing.

{% tab template="treegrid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { getValue } from '@syncfusion/ej2-base';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel, Page } from '@syncfusion/ej2-react-treegrid';
import { DialogEditEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];

  public actionBegin(args: DialogEditEventArgs): void {
    if (args.requestType === 'beginEdit') {
      if (getValue('Priority', args.rowData as object) === "Breaker") {
        args.cancel = true;
      }
    }
  }

  public render() {
    this.actionBegin = this.actionBegin.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={265}
       editSettings={this.editOptions} actionBegin={this.actionBegin} toolbar={this.toolbarOptions}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar, Page]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}