---
title: "Infinite Scrolling"
component: "Grid"
description: "Learn how to improve performance in the Essential JS 2 DataGrid control by using this infinite scroll feature. Also learn about the limitations of this feature."
---

# Infinite scrolling

Infinite scrolling is used to load a huge amount of data without degrading the Grid performance. This feature works like the lazy loading concept, which means the buffer data is loaded only when the scrollbar reaches the end of the scroller.

To enable Infinite scrolling, set `enableInfiniteScrolling` property as true.

> * In this feature, Grid will not make a new data request when you visit the same page again.

{% tab template="grid/virtual-scroll", sourceFiles="app/App.tsx,app/largeData.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { PageSettingsModel, InfiniteScroll, InfiniteScrollSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './largeData';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data(1000);
  public pageSettings: PageSettingsModel = { pageSize: 50 };
  public render() {
    return <GridComponent dataSource={this.data} height={300} enableInfiniteScrolling={true} pageSettings={ this.pageSettings }>
            <Inject services={[InfiniteScroll]} />
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'/>
                <ColumnDirective field='Engineer' width='100'/>
                <ColumnDirective field='Designation' width='100'/>
                <ColumnDirective field='Estimation' headerText='Estimation' textAlign='Right' width='100'/>
                <ColumnDirective field='Status' width='100'/>
            </ColumnsDirective>
            </GridComponent>
  }
}
```

{% endtab %}

## InitialBlocks

You can define the initial loading pages count by using `infiniteScrollSettings.initialBlocks` property. By default, this feature loads three pages in initial rendering.

In the below demo, we have changed this property value to load five page records instead of three.

{% tab template="grid/virtual-scroll", sourceFiles="app/App.tsx,app/largeData.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { PageSettingsModel, InfiniteScroll, InfiniteScrollSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './largeData';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data(1000);
  public pageSettings: PageSettingsModel = { pageSize: 50 };
  public infiniteOptions: InfiniteScrollSettingsModel = { initialBlocks: 5 };
  public render() {
    return <GridComponent dataSource={this.data} height={300} enableInfiniteScrolling={true} infiniteScrollSettings={ this.infiniteOptions } pageSettings={ this.pageSettings }>
            <Inject services={[InfiniteScroll]} />
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'/>
                <ColumnDirective field='Engineer' width='100'/>
                <ColumnDirective field='Designation' width='100'/>
                <ColumnDirective field='Estimation' headerText='Estimation' textAlign='Right' width='100'/>
                <ColumnDirective field='Status' width='100'/>
            </ColumnsDirective>
            </GridComponent>
  }
}
```

{% endtab %}

## Cache Mode

Cache is used to store the loaded rows object in the Grid instance which can be reused for creating the row elements whenever you scroll to already visited page. Also, this mode maintains row elements based on the `infiniteScrollSettings.maxBlocks` count value, once this limit exceeds then it will remove row elements from DOM for new rows.

To enable the cache mode in Infinite scrolling, set `infiniteScrollSettings.enableCache` property as true.

{% tab template="grid/virtual-scroll", sourceFiles="app/App.tsx,app/largeData.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { PageSettingsModel, InfiniteScroll, InfiniteScrollSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './largeData';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data(1000);
  public pageSettings: PageSettingsModel = { pageSize: 50 };
  public infiniteOptions: InfiniteScrollSettingsModel = { enableCache: true };
  public render() {
    return <GridComponent dataSource={this.data} height={300} enableInfiniteScrolling={true} infiniteScrollSettings={ this.infiniteOptions } pageSettings={ this.pageSettings }>
            <Inject services={[InfiniteScroll]} />
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'/>
                <ColumnDirective field='Engineer' width='100'/>
                <ColumnDirective field='Designation' width='100'/>
                <ColumnDirective field='Estimation' headerText='Estimation' textAlign='Right' width='100'/>
                <ColumnDirective field='Status' width='100'/>
            </ColumnsDirective>
            </GridComponent>
  }
}
```

{% endtab %}

## Limitations for Infinite Scrolling

* Due to the element height limitation in browsers, the maximum number of records loaded by the grid is limited due to the browser capability.
* Initial loading rows total height must be greater than the viewport height.
* Cell selection will not be persisted in cache mode.
* Infinite scrolling is not compatible with batch editing, detail template and hierarchy features.
* Group expand and collapse state will not be persisted in cache mode.
* The aggregated information and total group items are displayed based on the current view items. To get these information regardless of the view items, refer to the
[`Group with Page`](./grouping/#Group-with-paging) topic.
* Programmatic selection using the [`selectRows`](../api/grid/#selectrows) and [`selectRow`](../api/grid/#selectrow) method is not supported in infinite scrolling.
