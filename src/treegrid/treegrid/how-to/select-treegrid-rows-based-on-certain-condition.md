---
title: "Select treegrid rows based on certain condition"
component: "TreeGrid"
description: "Learn how to select rows in treegrid based on certain condition"
---

# Select treegrid rows based on certain condition

You can select the specific row in the treegrid based on a certain condition by using the [`selectRows`](../api/treegrid/#selectrows) method in the [`dataBound`](../api/treegrid/#databound) event of TreeGrid.

In the below demo, we have selected the grid rows only when *Duration* column value greater than *4*.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { getValue } from '@syncfusion/ej2-base';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Page, TreeGrid, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { RowDataBoundEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public selIndex: number[] = [];
  public treegrid: TreeGrid | null;
  public settings: SelectionSettingsModel = { type: 'Multiple' };
  public rowDataBound(args:RowDataBoundEventArgs):void {
    if (getValue('Duration', args.data as object) > 4) {
      this.selIndex.push(parseInt((args.row as HTMLTableRowElement)
        .getAttribute('aria-rowindex') as string, 0));
    }
  }
  public dataBound():void {
    if (this.treegrid && this.selIndex.length) {
        this.treegrid.selectRows(this.selIndex);
        this.selIndex = [];
    }
  }

  public render() {
    this.rowDataBound = this.rowDataBound.bind(this);
    this.dataBound = this.dataBound.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={280}
      allowPaging={true} ref={g => this.treegrid = g} rowDataBound={this.rowDataBound} dataBound={this.dataBound} selectionSettings={this.settings}>
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