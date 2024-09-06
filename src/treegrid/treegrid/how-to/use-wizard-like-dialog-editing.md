---
title: "Use Wizard like Dialog Editing"
component: "TreeGrid"
description: "Learn how to Use Wizard like Dialog Editing."
---

# Use Wizard like Dialog Editing

Wizard helps you create intuitive step-by-step forms to fill. You can achieve the wizard like editing by using the dialog template feature. It support your own editing template by defining [`editSettings.mode`](https://ej2.syncfusion.com/react/documentation/api/treegrid/editSettings/#mode) as **Dialog** and [`editSetting.template`](https://ej2.syncfusion.com/react/documentation/api/treegrid/editSettings/#template) as a REACT Component.

The following example demonstrate the wizard like editing in the treegrid with the obtrusive Validation.

{% tab template="treegrid/wizardediting", sourceFiles="app/App.tsx,app/datasource.tsx,app/wizardTemplate.tsx,app/projectModel.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { IProjectModel } from './projectModel';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel, Page, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import { DialogEditEventArgs } from '@syncfusion/ej2-react-grids';
import { DialogFormTemplate } from './wizardTemplate';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog', template: this.dialogTemplate.bind(this) };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  public treegrid: TreeGrid | null;

  public dialogTemplate(props: IProjectModel): any {
    const a = [props, this.treegrid]
    return (<DialogFormTemplate {...a} />);
  }

  public actionComplete(args: DialogEditEventArgs): void {
    // Set initial Focus
    if (args.requestType === 'beginEdit') {
      ((args.form as HTMLFormElement).elements.namedItem('TaskName') as HTMLInputElement).focus();
    } else if (args.requestType === 'add') {
      ((args.form as HTMLFormElement).elements.namedItem('TaskID')as HTMLInputElement).focus();
    }
  }

  public render() {
    this.actionComplete = this.actionComplete.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={265} toolbar={this.toolbarOptions}
       editSettings={this.editOptions}
       ref={g => this.treegrid = g} actionComplete ={this.actionComplete}>
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