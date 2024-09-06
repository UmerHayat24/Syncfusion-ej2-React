---
title: "Set complex column as Foreignkey column"
component: "Grid"
description: "Learn how to set complex column as Foreignkey column."
---

# Set complex column as Foreignkey column

The following example shows how to set the complex column as foreign key column.

In the following example, *Employee.EmployeeID* is a complex column and also declared as a foreign column which shows *FirstName* column from foreign data.

{% tab template="grid/foreign-key", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, ForeignKey, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public render() {
    return <GridComponent dataSource={data} height={315}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
        <ColumnDirective field='Employee.EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID'
        dataSource={employeeData}  headerText='Employee Name' width='150'/>
        <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
      </ColumnsDirective>
      <Inject services={[ForeignKey]} />
    </GridComponent>
  }
};
```

{% endtab %}