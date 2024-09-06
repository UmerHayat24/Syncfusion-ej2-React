---
title: "Provide custom data source and enabling filtering to DropDownList"
component: "TreeGrid"
description: "Learn how to Provide custom data source and enabling filtering to DropDownList."
---

# Provide custom data source and enabling filtering to DropDownList

You can provide data source to the DropDownList by using the **params** of [`columns.edit`](../api/treegrid/column/#edit) property.

While setting new data source using edit params, you must specify a new **query** property for the DropDownList as follows,

```typescript
  public priority : IEditCell = {
    params:   {
      actionComplete: () => false,
      allowFiltering: true,
      dataSource: new DataManager(this.priorityData),
      fields: { text: "countryName", value: "countryName"},
      query: new Query()
    }
  };
```

You can also enable filtering for the DropDownList by passing the [`allowFiltering`](../../api/drop-down-list/#allowfiltering) as **true** to the edit params.

In the below demo, DropDownList is rendered with custom [`dataSource`](../../api/drop-down-list/#datasource) for the *Priority* column and enabled filtering to search DropDownList items.

{% tab template="treegrid/cascade-drop", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel, Page } from '@syncfusion/ej2-react-treegrid';
import { IEditCell } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];

  public priorityData: object[] = [
    { priorityName: 'Normal', priorityId: '1' },
    { priorityName: 'High', priorityId: '2' },
    { priorityName: 'Low', priorityId: '3' },
    { priorityName: 'Critical', priorityId: '4' },
    { priorityName: 'Breaker', priorityId: '5' }
  ];

  public priority: IEditCell = {
    params:   {
      actionComplete: () => false,
      allowFiltering: true,
      dataSource: new DataManager(this.priorityData),
      fields: { text: "priorityName", value: "priorityName"},
      query: new Query()
    }
  }

  public render() {
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID'
       editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Priority' headerText='Priority' width='90' editType= 'dropdownedit' textAlign='Right' edit={this.priority} />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar, Page]} />
      </TreeGridComponent>
    );
  }
};

```

{% endtab %}