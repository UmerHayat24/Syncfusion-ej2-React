---
title: "Display null date values at always"
component: "TreeGrid"
description: "Learn how to display null date values at always."
---

# Display the null date values at bottom of the TreeGrid while perform sorting

By default the null values are displayed at bottom of the TreeGrid row while perform sorting in ascending order. As well as this values are displayed at top of the TreeGrid row while perform sorting with descending order. But you can customize this default order to display the null values at always bottom row of the TreeGrid by using [`column.sortComparer`](../api/treegrid/column/#sortcomparer) method.

In the below demo we have displayed the null date values at bottom of the Grid row while sorting the **StartDate** column in both ways.

{% tab template="treegrid/null-date-value", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject, Sort } from '@syncfusion/ej2-react-treegrid';
import { SortEventArgs } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component<{}, {action: string}> {
  constructor(props: any) {
    super(props);
    this.state = {action: ''};
  }
  // The custom function
  public sortComparer(reference: any, comparer: any) {
    const sortAsc = this.state.action === "Ascending" ? true : false;
    if (sortAsc && reference === null) {
        return -1;
    } else if (sortAsc && comparer === null) {
        return 1;
    } else if (!sortAsc && reference === null) {
        return -1;
    } else if (!sortAsc && comparer === null) {
        return 1;
    } else {
        return reference - comparer;
    }
};
public actionBegin(args: SortEventArgs): void {
    if (args.requestType === "sorting") {
      this.setState({action: args.direction as string});
    }
}

  public render() {
    this.actionBegin = this.actionBegin.bind(this);
    this.sortComparer = this.sortComparer.bind(this);
    return (
      <TreeGridComponent dataSource={projectData2} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID'
      allowSorting={true} actionBegin={this.actionBegin}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='70'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='70' sortComparer={this.sortComparer} format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='70' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Sort]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}