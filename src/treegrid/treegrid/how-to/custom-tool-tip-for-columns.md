---
title: "Custom Tooltip for columns"
component: "TreeGrid"
description: "Learn how to Custom Tooltip for columns."
---

# Custom Tooltip for columns

You can achieve the custom tooltip([`EJ2 Tooltip`](https://ej2.syncfusion.com/react/documentation/tooltip/getting-started)) for TreeGrid by using the [`queryCellInfo`](../api/treegrid/#querycellinfo) event.

Render the ToolTip component for the treegrid cells by using the following code in the
[`queryCellInfo`](../api/treegrid/#querycellinfo) event.

```typescript

  public tooltip(args: QueryCellInfoEventArgs){
    const tooltip: Tooltip = new Tooltip({
      content: getValue((args.column as Column).field, args.data as object).toString()
    });
    tooltip.appendTo(args.cell as HTMLElement);
  }

```

{% tab template="treegrid/custom-tooltip", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { getValue } from '@syncfusion/ej2-base';
import { Tooltip } from '@syncfusion/ej2-popups';
import { ColumnsDirective, ColumnDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { QueryCellInfoEventArgs, Column } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public tooltip(args: QueryCellInfoEventArgs){
    const tooltip: Tooltip = new Tooltip({
      content: getValue((args.column as Column).field, args.data as object).toString()
    });
    tooltip.appendTo(args.cell as HTMLElement);
  }
  public render() {
    this.tooltip = this.tooltip.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' queryCellInfo={this.tooltip} height={320}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
        </ColumnsDirective>
      </TreeGridComponent>
    );
  }
};

```

{% endtab %}