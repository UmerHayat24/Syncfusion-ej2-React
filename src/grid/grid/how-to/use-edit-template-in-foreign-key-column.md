---
title: "Use Edit Template in Foreign Key Column"
component: "Grid"
description: "Learn how to Use Edit Template in Foreign Key Column."
---

# Use Edit Template in Foreign Key Column

By default, foreign key column uses dropdown component for editing.
You can render other than the dropdown by using the [`column.edit`](../../api/grid/column/#edit) property.
The following example demonstrates the way of using edit template in foreign column.

In the following example, The *Employee Name* is a foreign key column and while editing,
AutoComplete component is rendered instead of DropDownList.

{% tab template="grid/foreign-key", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { createElement, getValue } from '@syncfusion/ej2-base';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { AutoComplete } from '@syncfusion/ej2-dropdowns';
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Column, Edit, ForeignKey, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public autoComplete: AutoComplete;
  public editOption: EditSettingsModel = {allowEditing: true};
  public toolbar: ToolbarItems[] = ['Edit', 'Update', 'Cancel'];
  public edit = {
    create: () => { // to create input element
      return createElement('input');
    },
    destroy: () => { // to destroy the custom component.
        this.autoComplete.destroy();
    },
    read: () => { // return edited value to update data source
      const value: object[] = new DataManager(employeeData).executeLocal(new Query().where('FirstName', 'equal', this.autoComplete.value));
      return value.length && getValue('EmployeeID', value[0]); // to convert foreign key value to local value.
    },
    write: (args: { rowData: object, column: Column, foreignKeyData: object, element: HTMLElement }) => { // to show the value for custom component
        this.autoComplete = new AutoComplete({
            dataSource: new DataManager(employeeData),
            fields: { value: args.column.foreignKeyValue },
            value: args.foreignKeyData[0][args.column.foreignKeyValue]
        });
        this.autoComplete.appendTo(args.element);
    }
  };
  public render() {
    return <GridComponent dataSource={data} height={280} editSettings= {this.editOption}
      toolbar={this.toolbar}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
        <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID'
        dataSource={employeeData}  headerText='Employee Name' width='150' edit={this.edit}/>
        <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2' editType='numericedit'/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
      </ColumnsDirective>
      <Inject services={[ForeignKey, Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}
