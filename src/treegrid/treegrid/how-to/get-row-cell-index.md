---
title: "Get specific row and cell index in TreeGrid"
component: "TreeGrid"
description: "Learn how to get specific row and cell index in TreeGrid."
---

# Get specific row and cell index in TreeGrid

You can get the specific row and cell index of the treegrid by using [`rowSelected`](../api/treegrid/#rowselected) event of the treegrid. Here, we can get the row and cell index by using *aria-rowindex* (get row Index from *tr* element) and *aria-colindex* (column index from *td* element) attribute.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject, Page } from '@syncfusion/ej2-react-treegrid';
import { RowSelectEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public rowSelected(args: RowSelectEventArgs):void {
    alert("row index: "+(args.row as HTMLTableRowElement).getAttribute('aria-rowindex'));
    alert("column index: "+(args.target as HTMLElement).getAttribute('aria-colindex'));
  }

  public render() {
    this.rowSelected = this.rowSelected.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' rowSelected={this.rowSelected} height={267}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Page]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}
