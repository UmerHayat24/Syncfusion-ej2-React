---
title: "Perform TreeGrid actions by keyboard shortcut keys"
component: "TreeGrid"
description: "Learn how to Perform TreeGrid actions by keyboard shortcut keys."
---

# Perform TreeGrid actions by keyboard shortcut keys

Using keyboard shortcuts, TreeGrid performs navigation and actions.

In addition, You can also perform treegrid actions with custom keyboard shortcuts. This operation has to be achieved outside of the treegrid with the help of **keydown** event.

The following example demonstrates on *Adding* a new row when **Enter** key is pressed in the treegrid.

{% tab template="treegrid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel, Page, TreeGrid } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  public treegrid: TreeGrid | null;

  public load(): void {
    if (this.treegrid) {
      this.treegrid.element.addEventListener('keydown', this.keyDownHandler);
    }
  }

  public keyDownHandler(e: any): void {
    if (this.treegrid && e.keyCode === 13) {
      this.treegrid.addRecord();
    }
  }

  public render() {
    this.load = this.load.bind(this);
    this.keyDownHandler = this.keyDownHandler.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={265}
       editSettings={this.editOptions} load={this.load} toolbar={this.toolbarOptions}
       ref={g => this.treegrid = g}>
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