---
title: "Infinite Scrolling"
component: "Tree Grid"
description: "Learn how to improve performance in the Essential JS 2 Tree Grid control by using infinite scroll feature. Also learn about the limitations of this feature."
---

# Infinite scrolling

Infinite scrolling is used to load a huge amount of data without degrading the Tree Grid performance. This feature works like the lazy loading concept, which means the buffer data is loaded only when the scrollbar reaches the end of the scroller.

To enable Infinite scrolling, set `enableInfiniteScrolling` property as true and inject **InfiniteScroll** module in Tree Grid.

> * In this feature, Tree Grid will not make a new data request when you visit the same page again.

{% tab template="treegrid/infinitescroll", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, InfiniteScroll } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { dataSource, virtualData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        dataSource();
        return <TreeGridComponent dataSource={virtualData} childMapping = 'Crew' enableInfiniteScrolling={true} treeColumnIndex={1} height='291'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD1' headerText='Player Name' width='120'></ColumnDirective>
                <ColumnDirective field='FIELD2' headerText='Year' width='100' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD3' headerText='Stint' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD4' headerText='TMID' width='120' textAlign='Right'></ColumnDirective>
            </ColumnsDirective>
                <Inject services={[InfiniteScroll]} />
        </TreeGridComponent>
    }
}
```

{% endtab %}

## InitialBlocks

You can define the initial loading pages count by using `infiniteScrollSettings.initialBlocks` property. By default, this feature loads three pages in initial rendering.

In the below demo, we have changed this property value to load five page records instead of three.

{% tab template="treegrid/infinitescroll", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, InfiniteScroll, InfiniteScrollSettingsModel, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { dataSource, virtualData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public pageSettings: PageSettingsModel = { pageSize: 50 };
  public infiniteOptions: InfiniteScrollSettingsModel = { initialBlocks: 5 };
  public render() {
    dataSource();
    return <TreeGridComponent dataSource={virtualData} childMapping = 'Crew' height={300} enableInfiniteScrolling={true} infiniteScrollSettings={ this.infiniteOptions } pageSettings={ this.pageSettings } treeColumnIndex={1}>
            <Inject services={[InfiniteScroll]} />
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD1' headerText='Player Name' width='120'></ColumnDirective>
                <ColumnDirective field='FIELD2' headerText='Year' width='100' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD3' headerText='Stint' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD4' headerText='TMID' width='120' textAlign='Right'></ColumnDirective>
            </ColumnsDirective>
          </TreeGridComponent>
  }
}
```

{% endtab %}

## Cache Mode

Cache is used to store the loaded rows object in the Tree Grid instance which can be reused for creating the row elements whenever you scroll to already visited page. Also, this mode maintains row elements based on the `infiniteScrollSettings.maxBlocks` count value, once this limit exceeds then it will remove row elements from DOM for new rows.

To enable the cache mode in Infinite scrolling, set `infiniteScrollSettings.enableCache` property as true.

{% tab template="treegrid/infinitescroll", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, InfiniteScroll, InfiniteScrollSettingsModel, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { dataSource, virtualData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public pageSettings: PageSettingsModel = { pageSize: 50 };
  public infiniteOptions: InfiniteScrollSettingsModel = { enableCache: true };
  public render() {
    dataSource();
    return <TreeGridComponent dataSource={virtualData} childMapping = 'Crew' height={300} enableInfiniteScrolling={true} infiniteScrollSettings={ this.infiniteOptions } pageSettings={ this.pageSettings } treeColumnIndex={1}>
            <Inject services={[InfiniteScroll]} />
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD1' headerText='Player Name' width='120'></ColumnDirective>
                <ColumnDirective field='FIELD2' headerText='Year' width='100' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD3' headerText='Stint' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='FIELD4' headerText='TMID' width='120' textAlign='Right'></ColumnDirective>
            </ColumnsDirective>
          </TreeGridComponent>
  }
}
```

{% endtab %}

## Limitations for Infinite Scrolling

* Due to the element height limitation in browsers, the maximum number of records loaded by the tree grid is limited due to the browser capability.
* Initial loading rows total height must be greater than the viewport height.
* Cell selection will not be persisted in cache mode.
* Infinite scrolling is not compatible with batch editing, detail template.
* The aggregated information and total group items are displayed based on the current view items. To get these information regardless of the view items, refer to the
* Programmatic selection using the [`selectRows`](../api/treegrid/#selectrows) and [`selectRow`](../api/treegrid/#selectrow) method is not supported in infinite scrolling.
