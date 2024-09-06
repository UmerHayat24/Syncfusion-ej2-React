---
title: "Collapse all grouped rows at initial render"
component: "Grid"
description: "Learn how to collapse all grouped rows at initial render."
---

# Collapse all grouped rows at initial render

You can collapse all the grouped rows at initial rendering by using [`dataBound`](../../api/grid/#databound) event with  [`collapseAll`](../../api/grid/group/#collapseall) method of the grid.

In the below demo, all the grouped rows are collapsed at initial rendering.

 {% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Grid, Group, GroupSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public initial = true;
  public groupOptions : GroupSettingsModel = { columns: ['ShipCity'] };
  public gridObj: Grid | null;

  public dataBound():void {
    if (this.gridObj && this.initial === true) {
      this.gridObj.groupModule.collapseAll();
      this.initial = false;
    }
  }

  public render(){
    this.dataBound = this.dataBound.bind(this);
    return <GridComponent  dataSource={data} ref={grid => this.gridObj = grid} dataBound={this.dataBound}
      allowGrouping={true} groupSettings={this.groupOptions} height={267}>
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
        <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
        <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
      </ColumnsDirective>
      <Inject services={[Group]}/>
    </GridComponent >
    }
};
```

{% endtab %}