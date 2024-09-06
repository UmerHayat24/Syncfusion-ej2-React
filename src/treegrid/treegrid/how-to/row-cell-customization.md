---
title: "Row and Cell Customization in TreeGrid"
component: "TreeGrid"
description: "Learn how to customize the row and cell in treegrid"
---

# Row and Cell Customization in TreeGrid

In TreeGrid we can customize the row and cell using [`queryCellInfo`](../api/treegrid/#querycellinfo) and [`rowDataBound`](../api/treegrid/#rowdatabound) events of treegrid.

In the below demo, we customize and show the command buttons only for the parent rows using [`queryCellInfo`](../api/treegrid/#querycellinfo) and [`rowDataBound`](../api/treegrid/#rowdatabound) events of treegrid.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { sampleData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, CommandColumn, Inject } from '@syncfusion/ej2-react-treegrid';
import { Page, ITreeData } from '@syncfusion/ej2-react-treegrid';
import { QueryCellInfoEventArgs, RowDataBoundEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component<{}, {action: string}> {

  public treegrid: TreeGridComponent | null;
  public commands: any = [{ buttonOption: { content: ' Details', click: onclick } }];
  public queryCellInfo(args: QueryCellInfoEventArgs): void {
    if (!(args.data as ITreeData).hasChildRecords){
      if ((args.cell as HTMLElement).classList.contains("e-unboundcell")) {
        ((args.cell as HTMLElement).querySelector('.e-unboundcelldiv') as HTMLElement).style.display = "none"
      }
    }
  }

  public rowDataBound(args: RowDataBoundEventArgs): void {
    if (!(args.data as ITreeData).hasChildRecords) {
      (args.row as HTMLElement).style.backgroundColor = 'green';
    }
  }
  public render() {
    this.queryCellInfo = this.queryCellInfo.bind(this);
    this.rowDataBound = this.rowDataBound.bind(this);
    return (
      <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
      height={280} ref={g => this.treegrid = g} queryCellInfo={this.queryCellInfo.bind(this)}
      rowDataBound={this.rowDataBound.bind(this)}>
      <ColumnsDirective>
        <ColumnDirective field='taskID' headerText='Task ID' width='80' textAlign='Right'
          isPrimaryKey={true}></ColumnDirective>
        <ColumnDirective field='taskName' headerText='Task Name' width='200'></ColumnDirective>
        <ColumnDirective field='startDate' headerText='Start Date' width='140' textAlign='Right' format='yMd' type='date' />
        <ColumnDirective field='endDate' headerText='End Date' width='140' textAlign='Right' format='yMd' type='date' />
        <ColumnDirective field='duration' headerText='Duration' width='90' textAlign='Right' />
        <ColumnDirective field='progress' headerText='Progress' width='90' textAlign='Right'/>
        <ColumnDirective headerText='Custom Button' width='160' commands={this.commands}></ColumnDirective>
      </ColumnsDirective>
        <Inject services={[Page, CommandColumn]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}