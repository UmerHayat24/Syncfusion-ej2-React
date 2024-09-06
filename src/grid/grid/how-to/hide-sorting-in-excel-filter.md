---
title: "Hide sorting options on excel filter Dialog"
component: "Grid"
description: "Learn how to hide sorting options in excel filter Dialog."
---

# Hide sorting options on excel filter Dialog

You can hide the sorting options on the excel filter dialog by setting display as none for the following classes.

```css
    .e-excel-ascending,
    .e-excel-descending,
    .e-separator.e-excel-separator {
    display: none;
    }
```

{% tab template="grid/disable-sorting-excel", sourceFiles="app/App.tsx,app/datasource.tsx" %}

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
  public filterOptions: any = {type: 'Excel'};

  public render() {
    return <GridComponent dataSource={data} height={280} allowFiltering={true} filterSettings={this.filterOptions} ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
          <ColumnDirective field='EmployeeID'  headerText='EmployeeID' width='100' textAlign="Right" />
          <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
        </ColumnsDirective>
        <Inject services={[Filter]} />
      </GridComponent>
    }
};
```

{% endtab %}
