---
title: "Perform aggregation in Foreign Key Column"
component: "Grid"
description: "Learn how to Perform aggregation in Foreign Key Column."
---

# Perform aggregation in Foreign Key Column

Default aggregations are not supported in a foreign key column.
You can achieve aggregation for the foreign key column by using the custom aggregates.
The following example demonstrates the way to achieve aggregation in foreign key column.

In the following example, The *Employee Name* is a foreign key column and the aggregation for the foreign column was calculated in customAggregateFn.

{% tab template="grid/foreign-key", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Aggregate, Column, ForeignKey, getForeignData, Grid } from '@syncfusion/ej2-react-grids';
import { AggregateColumnDirective, AggregateColumnsDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {action: string}> {
  public grid: Grid | null;
  public custom(props: any): any {
    return(<span>Count of Margaret: {props.Custom}</span>)
  }
  // Custom Aggregate function for foreign column
  public customAggregateFn(args: any, column: Column) {
    const proxy: Grid = this.grid as Grid;
    return args.result.filter((dObj: object) => {
      return getValue('FirstName' ,
        getForeignData(proxy.getColumnByField(column.field), dObj)[0]) === 'Margaret';
    }).length;
  };
  public render() {
    this.customAggregateFn = this.customAggregateFn.bind(this);
    return <GridComponent dataSource={data} height={280} ref={g => this.grid = g}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign='Right'/>
        <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID'
        dataSource={employeeData}  headerText='Employee Name' width='150'/>
        <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
      </ColumnsDirective>
      <AggregatesDirective>
          <AggregateDirective>
            <AggregateColumnsDirective>
              <AggregateColumnDirective field='EmployeeID' type='Custom'
                customAggregate ={this.customAggregateFn} footerTemplate={this.custom} />
            </AggregateColumnsDirective>
          </AggregateDirective>
        </AggregatesDirective>
      <Inject services={[ForeignKey, Aggregate]} />
    </GridComponent>
  }
}
```

{% endtab %}
