---
title: "Frozen"
component: "Grid"
description: "Learn how to freeze the grid columns at left or right side and how to freeze the grid rows at top."
---

# Frozen rows and columns

Frozen rows and columns provides an option to make rows and columns always visible in the top and left side of the grid while scrolling.

To use frozen rows and columns support, inject the **Freeze** module in the Grid.

In this demo, the [`frozenColumns`](../api/grid/#frozencolumns) is set as **'2'** and the [`frozenRows`](../api/grid/#frozenrows)
is set as **'3'**. Hence, the left two columns and top three rows are frozen.

{% tab template="grid/scrolling", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Freeze, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return (<div>
          <GridComponent dataSource={data} height="315" frozenRows={3} frozenColumns={2}
            allowSelection={false} enableHover={false}>
            <ColumnsDirective>
             <ColumnDirective field='OrderID' width='120' textAlign='Right'/>
             <ColumnDirective field='CustomerID' width='150'/>
             <ColumnDirective field='OrderDate' width='130' format='yMd' textAlign='Right'/>
             <ColumnDirective field='EmployeeID' width='120' textAlign="Right"/>
             <ColumnDirective field='ShipName' width='150'/>
             <ColumnDirective field='ShipAddress' width='170'/>
             <ColumnDirective field='ShipCity' width='150'/>
             <ColumnDirective field='ShipCountry' width='150'/>
             <ColumnDirective field='ShipRegion' width='150'/>
             <ColumnDirective field='ShipPostalCode' width='150'/>
             <ColumnDirective field='Freight' width='120'/>
            </ColumnsDirective>
            <Inject services={[Freeze]} />
           </GridComponent></div>)
  }
};
```

{% endtab %}

> Frozen rows and columns should not be set outside the grid view port.
> Frozen Grid will support row and column virtualization feature, which helps to improve the Grid performance while loading a large dataset.

## Limitations of Frozen Grid

The following features are not supported in frozen rows and columns:

* Grouping
* Row Template
* Detail Template
* Hierarchy Grid

## Freeze Direction

You can freeze the Grid columns on the left or right side by using the [`column.freeze`](../api/grid/column/#freeze) property and the remaining columns will be movable. The grid will automatically move the columns to the left or right position based on the [`column.freeze`](../api/grid/column/#freeze) value.

Types of the [`column.freeze`](../api/grid/column/#freeze) directions:

* **`Left`**: Allows you to freeze the columns at the left.
* **`Right`**: Allows you to freeze the columns at the right.

In this demo, the **ShipCountry** column is frozen at the left and the **CustomerID** column is frozen at the right side of the content table.

{% tab template="grid/scrolling", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Freeze, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return (<div>
          <GridComponent dataSource={data} height="315" frozenRows={2} enableHover={false}>
            <ColumnsDirective>
             <ColumnDirective field='OrderID' width='120' textAlign='Right'/>
             <ColumnDirective field='Freight' width='120'/>
             <ColumnDirective field='CustomerID' width='150' freeze='Right'/>
             <ColumnDirective field='OrderDate' width='130' format='yMd' textAlign='Right'/>
             <ColumnDirective field='ShipName' width='150'/>
             <ColumnDirective field='ShipAddress' width='170'/>
             <ColumnDirective field='ShipCity' width='150'/>
             <ColumnDirective field='ShipCountry' width='150' freeze='Left'/>
            </ColumnsDirective>
            <Inject services={[Freeze]} />
           </GridComponent></div>)
  }
};
```

{% endtab %}

> * Freeze Direction is not compatible with the [`isFrozen`](../api/grid/column/#isfrozen) and [`frozenColumns`](../api/grid/#frozencolumns) properties.

## Limitations of Freeze Direction

This feature has the below limitations, along with the above mentioned Frozen Grid limitations.

* Column virtualization
* Infinite scroll cache mode
* Freeze direction in the stacked header is not compatible with column reordering.
