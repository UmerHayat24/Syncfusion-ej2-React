---
title: "Display null date values at always"
component: "Grid"
description: "Learn how to display null date values at always."
---

# Display the null date values at bottom of the Grid while perform sorting

By default the null values are displayed at bottom of the Grid row while perform sorting in ascending order. As well as this values are displayed at top of the Grid row while perform sorting with descending order. But you can customize this default order to display the null values at always bottom row of the Grid by using [`column.sortComparer`](../../api/grid/column/#sortcomparer) method.

In the below demo we have displayed the null date values at bottom of the Grid row while sorting the **OrderDate** column in both ways.

{% tab template="grid/null-date-value", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Sort, SortEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {action: string}> {
    constructor(props: any) {
      super(props);
      this.state = {action: ''};
    }
    // The custom function
    public sortComparer(reference: any, comparer: any) {
        const sortAsc = this.state.action === "Ascending" ? true : false;
        if (sortAsc && reference === null) {
            return 1;
        } else if (sortAsc && comparer === null) {
            return -1;
        } else if (!sortAsc && reference === null) {
            return -1;
        } else if (!sortAsc && comparer === null) {
            return 1;
        } else {
            return reference - comparer;
        }
    };
    public actionBegin(args: SortEventArgs): void {
        if (args.requestType === "sorting") {
          this.setState({action: args.direction as string});
        }
    }
    public render() {
      this.actionBegin = this.actionBegin.bind(this);
      this.sortComparer = this.sortComparer.bind(this);
      return <GridComponent id='grid' dataSource={data} allowSorting={true} actionBegin={this.actionBegin}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
            <ColumnDirective field='OrderDate' headerText='Order Date' format='yMd' sortComparer={this.sortComparer} width='120'/>
            <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[Sort]} />
      </GridComponent>
    }
}
```

{% endtab %}