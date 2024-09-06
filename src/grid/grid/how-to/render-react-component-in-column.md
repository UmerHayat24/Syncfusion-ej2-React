---
title: "Render React component in a column"
component: "Grid"
description: "Learn how to Render React component in a column."
---

# Render React component in a column

You can use [`queryCellInfo`](../../api/grid/#querycellinfo) event to render the React component inside Grid cells.
In the following sample, the DropDownList is rendered in the **ShipCountry** column

{% tab template="grid/dropdown-component", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataUtil } from '@syncfusion/ej2-data';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { Column, ColumnDirective, ColumnsDirective, GridComponent, QueryCellInfoEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public drop: string[] = DataUtil.distinct(data, 'ShipCountry') as string[];
  public dropdown(args: QueryCellInfoEventArgs) {
    if((args.column as Column).field === "ShipCountry") {
      const val = getValue((args.column as Column).field, args.data);
      ReactDOM.render(<DropDownListComponent id="dropdown"value={val} dataSource={this.drop} change={this.onChange}/>, args.cell as Element)
    }
  }
  public onChange(args: ChangeEventArgs){
    /** Event will trigger when you have change the value in dropdown column */
    alert(args.value)
  }

  public render() {
    this.dropdown = this.dropdown.bind(this);
    return (<div>
    <GridComponent dataSource={data} height={315} queryCellInfo={this.dropdown} >
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
        <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
      </ColumnsDirective>
    </GridComponent>
    </div>)
  }
};
```

{% endtab %}