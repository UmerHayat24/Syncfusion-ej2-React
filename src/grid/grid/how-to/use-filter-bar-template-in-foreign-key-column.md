---
title: "Use filter bar template in foreign key column"
component: "Grid"
description: "Learn how to Use filter bar template in foreign key column."
---

# Use filter bar template in foreign key column

You can use the filter bar template in foreign key column by defining the
[`column.filterBarTemplate`](../../api/grid/column//#filterbartemplate) property.
The following example demonstrates the way to use filter bar template in foreign column.

In the following example, The **Employee Name** is a foreign key column.
This column header shows the custom filter bar template and you can select filter value by using the *DropDown* options.

{% tab template="grid/foreign-key", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import { DataManager } from '@syncfusion/ej2-data';
import { ChangeEventArgs, DropDownList } from '@syncfusion/ej2-dropdowns';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Column, Filter, ForeignKey, Grid } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public filterBarTemplate = {
    create: (args: { element: Element, column: Column }) => {
        return createElement('input', { className: 'flm-input' });
    },
    write: (args: { element: Element, column: Column }) => {
      employeeData.splice(0, 0, {'FirstName': 'All'}); // for clear filtering
      const dropInstance: DropDownList = new DropDownList({
        change: (arg: ChangeEventArgs) => {
          if (this.grid) {
            if (arg.value !== 'All') {
              this.grid.filterByColumn('EmployeeID', 'equal', arg.value);
            }
            else {
              this.grid.removeFilteredColsByField('EmployeeID');
            }
          }
        },
        dataSource: new DataManager(employeeData),
        fields: { text: 'FirstName' },
        index: 0,
        placeholder: 'Select a value',
        popupHeight: '200px'
      });
      dropInstance.appendTo(args.element as HTMLElement);
    }
  };

  public render() {
    return <GridComponent dataSource={data} height={280} allowFiltering={true} ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
          <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID'
           dataSource={employeeData}  headerText='Employee Name' width='150' filterBarTemplate={this.filterBarTemplate}/>
          <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
        </ColumnsDirective>
        <Inject services={[ForeignKey, Filter]} />
      </GridComponent>
    }
};
```

{% endtab %}
