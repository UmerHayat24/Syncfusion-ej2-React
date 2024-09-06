---
title: "Display ForeignKey value at initial rendering in TreeGrid"
component: "TreeGrid"
description: "Learn how to display ForeignKey value at initial rendering in TreeGrid."
---

# Display ForeignKey value at initial rendering in TreeGrid

Since TreeGrid Databinding concept is of hierarchy relationship, we do not provide in-built support for foreignkey datasource.

To display the foreignKey value at initial rendering, we can use the [`queryCellInfo`](../api/treegrid/#querycellinfo) event of the treegrid and also by using the [`editType`](../api/treegrid/column/#edittype) and [`columns.edit`](../api/treegrid/column/#edit) properties of TreeGrid Column, we can render Dropdownlist with external or foreign dataSource.

{% tab template="treegrid/foreignkey", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { foreignKeyData } from './datasource';
import { dropData } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Page, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { QueryCellInfoEventArgs, Column, IEditCell } from '@syncfusion/ej2-react-grids';

/* tslint:disable */
export default class App extends React.Component<{}, {action: string}> {

  public treegrid: TreeGridComponent | null;
  public editSettings: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];
  public queryCellInfo(args: QueryCellInfoEventArgs): void {
    if ((args.column as Column).field === "EmployeeID") {
      for (var i = 0; i < dropData.length; i++) {
        let data: Object = args.data as Object;
        if (data[(args.column as Column).field] === dropData[i]["EmployeeID"]) {
          (args.cell as HTMLElement).innerText = dropData[i]["EmployeeName"]; // assign the foreignkey field value to the innertext
        }
      }
    }
  }

 // Bind ForeignKey DataSource for dropdown using editParams
  public employeeParams : IEditCell = {
    params:   {
      dataSource: new DataManager(dropData),
      fields: { text: "EmployeeName", value: "EmployeeID"},
      query: new Query()
    }
  };
  public render() {
    this.queryCellInfo = this.queryCellInfo.bind(this);
    return (
      <TreeGridComponent dataSource={foreignKeyData} treeColumnIndex={0} childMapping='Children'
      height={280} toolbar={this.toolbarOptions} editSettings={this.editSettings}
      ref={g => this.treegrid = g} queryCellInfo={this.queryCellInfo.bind(this)}>
        <ColumnsDirective>
          <ColumnDirective field='EmpID' headerText='EmpID' isPrimaryKey={true} width='70'></ColumnDirective>
          <ColumnDirective field='Name' headerText='Employee Name' width='70' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='Contact' headerText='Contact' width='90' textAlign='Right' />
          <ColumnDirective field='DOB' headerText='DOB' width='70' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='70' editType='dropdownedit' edit={this.employeeParams}></ColumnDirective>
          <ColumnDirective field='Country' headerText='Country' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Page, Edit, Toolbar]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}