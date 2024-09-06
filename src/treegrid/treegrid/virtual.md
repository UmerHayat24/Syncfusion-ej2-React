---
title: "Virtualization"
component: "TreeGrid"
description: "Learn how to improve performance in the Essential JS 2 TreeGrid control by using row with virtualization. Also learn about the limitations of virtualization."
---

# Virtualization

TreeGrid allows you to load large amount of data without performance degradation.

To use virtualization, you need to inject `VirtualScrollService` in TreeGrid.

## Row Virtualization

Row virtualization allows you to load and render rows only in the content viewport. It is an alternative way of paging in which the rows will be appended while scrolling vertically. To setup the row virtualization, you need to define
[`enableVirtualization`](../api/treegrid/#enablevirtualization) as true and content height by [`height`](../api/treegrid/#height) property.

The number of records displayed in the TreeGrid is determined implicitly by height of the content area and a buffer records will be maintained in the TreeGrid content in addition to the original set of rows.

Expand and Collapse state of any child record will be persisted.

{% tab template="treegrid/virtualscroll", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, VirtualScroll } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { dataSource, virtualData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        dataSource();
        return <TreeGridComponent dataSource={virtualData} childMapping = 'Crew' enableVirtualization={true} treeColumnIndex={1} height='291'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD1' headerText='Player Name' width='120'></ColumnDirective>
                <ColumnDirective field='FIELD2' headerText='Year' width='100' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD3' headerText='Stint' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD4' headerText='TMID' width='120' textAlign='Right'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[VirtualScroll]} />
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Limitations for Virtualization

* Due to the element height limitation in browsers, the maximum number of records loaded by the treegrid is limited by the browser capability.
* Cell selection will not be persisted in row.
* Virtual scrolling is not compatible with detail template, editing and row drag and drop features.
* Row count of the page is not depend on the **pageSize** property of the **pageSettings**. Row count for the page is determined by the [`height`](https://ej2.syncfusion.com/react/documentation/api/treegrid/#height) given to the TreeGrid.
* The virtual height of the treegrid content is calculated using the row height and total number of records in the data source and hence features which changes row height such as text wrapping are not supported. If you want to increase the row height to accommodate the content then you can specify the row height as below to ensure all the table rows are in same height.
* Programmatic selection using the **selectRows** method is not supported in virtual scrolling.
* Frozen column feature is not supported with Virtual Scrolling.