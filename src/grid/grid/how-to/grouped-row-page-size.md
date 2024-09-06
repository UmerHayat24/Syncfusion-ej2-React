---
title: "How to show grouped rows based on the pageSize"
component: "Grid"
description: "Learn how to show the grouped row based on the pageSize"
---

# How to show grouped rows based on the pageSize

By default, we have displayed the no of records based on the [`pageSize`](../../api/grid/pageSettings/#pagesize). If you want to show grouped column rows based on the [`pageSize`](../../api/grid/pageSettings/#pagesize) then we suggest you to use the below way.

In the below sample, we have overridden the default *generateQuery* to display the grouped rows instead of grid rows based on the  [`pageSize`](../../api/grid/pageSettings/#pagesize).

{% tab template="grid/group", sourceFiles="app/App.tsx,app/extendData.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Data, Grid, Group, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';
import { PagedData } from './extendData';

Data.prototype = PagedData.prototype;

export default class App extends React.Component<{}, {}>{
    public grid: Grid | null;
    public groupOptions: object = { columns: ['ShipCountry'] };
    public pageSettings: object = { pageSize: 5 };

    public render() {
      return <GridComponent ref={g => this.grid = g}  allowGrouping={true}
        groupSettings={this.groupOptions} allowPaging = {true} pageSettings = {this.pageSettings}
        dataSource={data}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
          <ColumnDirective field='CustomerID' width='100'/>
          <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
          <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Group, Page]} />
      </GridComponent>
    }
};
```

{% endtab %}