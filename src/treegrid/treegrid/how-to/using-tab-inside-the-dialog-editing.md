---
title: "Using Tab Inside the Dialog Editing"
component: "TreeGrid"
description: "Learn how to Using Tab Inside the Dialog Editing."
---

# Using Tab Inside the Dialog Editing

You can use [`tab`](../../../tab) component inside dialog edit UI using dialog template feature. The dialog template feature can be enabled by defining [`editSettings.mode`](../api/treegrid/editSettings/#mode) as `Dialog` and [`editSetting.template`](../api/treegrid/editSettings/#template) as a REACT Component.

The following example demonstrate the usage of tab control inside the dialog template.

{% tab template="treegrid/tabediting", sourceFiles="app/App.tsx,app/datasource.tsx,app/wizardTab.tsx,app/projectModel.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { IProjectModel } from './projectModel';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel, Page, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import { DialogFormTemplate } from './wizardTab';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog', template: this.dialogTemplate.bind(this) };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  public treegrid: TreeGrid | null;

  public dialogTemplate(props: IProjectModel): any {
    const a = [props, this.treegrid]
    return (<DialogFormTemplate {...a} />);
  }

  public render() {
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={265}
       editSettings={this.editOptions} toolbar={this.toolbarOptions}
       ref={g => this.treegrid = g}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar, Page]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}