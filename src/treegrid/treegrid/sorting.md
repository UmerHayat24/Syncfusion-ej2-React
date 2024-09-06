---
title: "Sorting"
component: "TreeGrid"
description: "Learn how to sort rows in the Essential JS 2 TreeGrid control, perform initial sorting, and customize sorting logic."
---

# Sorting

Sorting enables you to sort data in the *Ascending* or *Descending* order.
To sort a column, click the column header.

To sort multiple columns, press and hold the CTRL key and click the column header.  You can clear sorting of any one of the multi-sorted columns by pressing and holding the SHIFT key and clicking the specific column header.

To enable sorting in the TreeGrid, set the [`allowSorting`](../api/treegrid/#allowsorting) to true. Sorting options can be configured through the [`sortSettings`](../api/treegrid/sortSettings).

To use Sorting, inject **Sort** module in TreeGrid.

{% tab template="treegrid/sorting", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Sort, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping='subtasks' allowSorting='true' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='140'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='180'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='150' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='units' headerText='Units' width='90' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Sort]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * TreeGrid columns are sorted in the **Ascending** order. If you click the already sorted column, the sort direction toggles.
> * You can apply and clear sorting by invoking [`sortByColumn`](../api/treegrid#sortbycolumn) and [`clearSorting`](../api/treegrid/#clearsorting) methods.
> * To disable sorting for a particular column, set the [`columns.allowSorting`](../api/treegrid/#allowSorting) to *false*.

## Initial Sort

To sort at initial rendering, set the [`field`](../api/treegrid/sortDescriptorModel/#field) and [`direction`](../api/treegrid/sortDescriptorModel/#direction) in the [`sortSettings.columns`](../api/treegrid/sortSettings/#columns).

{% tab template="treegrid/sorting", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Sort, SortSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public sortingOptions: SortSettingsModel = {
        columns: [
            { field: 'Category', direction: 'Ascending' },
            { field: 'orderName', direction: 'Ascending' }
        ]
    };

    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping='subtasks' allowSorting='true' height='315' sortSettings={this.sortingOptions}>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='140'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='200'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='150' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='units' headerText='Units' width='90' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Sort]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Sorting Events

During the sort action, the treegrid component triggers two events. The [`actionBegin`](../api/treegrid/#actionbegin) event triggers before the sort action starts, and the [`actionComplete`](../api/treegrid/#actioncomplete) event triggers after the sort action is completed. Using these events you can perform the needed actions.

{% tab template="treegrid/sorting", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ActionEventArgs } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, Sort, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public actionHandler (args: ActionEventArgs) {
        /** custom Action */
        alert(args.requestType + ' ' + args.type);
    }

    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping='subtasks'
        allowSorting='true' height='315' actionBegin={this.actionHandler}
            actionComplete={this.actionHandler}>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='140'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='200'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='120' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='units' headerText='Units' width='90' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Sort]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> The `args.requestType` is the current action name. For example, in sorting the `args.requestType` value is *sorting*.

## Custom sort comparer

You can customize the default sort action for a column by defining the [`column.sortComparer`](../api/treegrid/column/#sortcomparer) property. The sort comparer function has the same functionality like [`Array.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sort comparer.

In the following example, custom sort comparer function was defined in the *Category* column.

{% tab template="treegrid/sorting", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Sort, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './datasource';

export default class App extends React.Component<{}, {}>{

    /** Custom comparer function */
    public sortComparer(reference: string, comparer:  string) {
        if (reference < comparer) {
            return -1;
        }
        if (reference > comparer) {
            return 1;
        }
        return 0;
    };

    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping='subtasks' allowSorting='true' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='140'/>
              <ColumnDirective field='orderName' headerText='Order Name' sortComparer={this.sortComparer} width='200'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='120' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='units' headerText='Units' width='90' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Sort]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> The sort comparer function will work only for the local data.

## Touch Interaction

When you tap the treegrid header on touchscreen devices, the selected column header is sorted. A popup ![Multi column sorting](images/sorting.jpg) is displayed for multi-column sorting. To sort multiple columns, tap the popup![Multi sorting](images/msorting.jpg), and then tap the desired treegrid headers.

The following screenshot shows treegrid touch sorting.

<!-- markdownlint-disable MD033 -->
<img src="../images/touch-sorting.jpg" alt="Touch Sorting" style="width:320px;height: 620px">
<!-- markdownlint-enable MD033 -->
