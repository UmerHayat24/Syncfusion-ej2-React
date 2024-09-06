---
title: "Customize filter UI in foreign key column"
component: "Grid"
description: "Learn how to Customize filter UI in foreign key column."
---

# Customize filter UI in foreign key column

You can create your own filtering UI by using [`column.filter`](../../api/grid/column/#filter) property.
The following example demonstrates the way to create a custom filtering UI in the foreign column.

In the following example, The **Employee Name** is a foreign key column. DropDownList is rendered using Filter UI.

{% tab template="grid/foreign-key", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import { DataManager } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Column, Filter, FilterSettingsModel, ForeignKey } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public dropInstance: DropDownList;
  public filterOption: FilterSettingsModel= {type: 'Menu'};
  public filter = {
    ui: {
        create: (args: { target: Element, column: Column }) => {
          const flValInput: HTMLElement = createElement('input', { className: 'flm-input' });
          args.target.appendChild(flValInput);
          this.dropInstance = new DropDownList({
              dataSource: new DataManager(employeeData),
              fields: { text: 'FirstName', value: 'EmployeeID' },
              placeholder: 'Select a value',
              popupHeight: '200px'
          });
          this.dropInstance.appendTo(flValInput);
        },
        read: (args: { target: Element, column: Column, operator: string, fltrObj: Filter }) => {
          args.fltrObj.filterByColumn(args.column.field, args.operator, this.dropInstance.text);
        },
        write: (args: {
          column: object, target: Element, parent: any,
          filteredValue: string
        }) => {
          this.dropInstance.text = (args.filteredValue || '');
        }
    }
  };

  public render() {
    return <GridComponent dataSource={data} height={315} allowFiltering={true}
    filterSettings={this.filterOption}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
        <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID'
        dataSource={employeeData}  headerText='Employee Name' width='150' filter={this.filter}/>
        <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
      </ColumnsDirective>
      <Inject services={[ForeignKey, Filter]} />
    </GridComponent>
  }
};
```

{% endtab %}
