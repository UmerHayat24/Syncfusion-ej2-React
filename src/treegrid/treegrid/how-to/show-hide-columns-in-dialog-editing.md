---
title: "Show or Hide columns in Dialog editing"
component: "TreeGrid"
description: "Learn how to Show or Hide columns in Dialog editing."
---

# Show or Hide columns in Dialog editing

You can show hidden columns or hide visible column's editor in the dialog while editing the treegrid record using [`actionBegin`](../../api/treegrid/#actionbegin) and [`actionComplete`](../../api/treegrid/#actioncomplete) events.

In the [`actionBegin`](../../api/treegrid/#actionbegin) event, based on **requestType** as **beginEdit** or  **add**. We can show or hide the editor by using [`column.visible`](../../api/treegrid/column/#visible) property.

In the [`actionComplete`](../../api/treegrid/#actioncomplete) event, based on **requestType** as **save**. We can reset the properties back to the column state.

In the below example, we have rendered the treegrid columns *Progress* as hidden column and *Priority* as visible column. In the edit mode, we have changed the *Progress* column to visible state and *Priority* column to hidden state.

{% tab template="treegrid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Column, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { DialogEditEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  public treegridObj: TreeGridComponent | null;

  public actionBegin(args: DialogEditEventArgs): void {
    if (this.treegridObj && (args.requestType === 'beginEdit' || args.requestType === 'add')) {
      const cols: Column[] = this.treegridObj.columns as Column[];
      for (const col of cols) {
        if (col.field === "Progress") {
          col.visible = true;
        }
        else if (col.field === "Priority") {
          col.visible = false;
        }
      }
    }
  }
  public actionComplete(args: DialogEditEventArgs): void {
    if (this.treegridObj && args.requestType === 'save') {
      const cols: Column[] = this.treegridObj.columns as Column[];
      for (const col of cols) {
        if (col.field === "Progress") {
          col.visible = false;
        }
        else if (col.field === "Priority") {
          col.visible = true;
        }
      }
    }
  }

  public render() {
    this.actionBegin = this.actionBegin.bind(this);
    this.actionComplete = this.actionComplete.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' actionComplete={this.actionComplete} editSettings={this.editOptions} toolbar={this.toolbarOptions}
      actionBegin={this.actionBegin} ref={g => this.treegridObj = g}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' visible={false} />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar]} />
      </TreeGridComponent>
    );
  }
};

```

{% endtab %}
