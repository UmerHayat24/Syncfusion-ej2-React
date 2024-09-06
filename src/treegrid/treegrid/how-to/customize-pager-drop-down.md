---
title: "Customize Pager DropDown"
component: "TreeGrid"
description: "Learn how to Customize Pager DropDown."
---

# Customize Pager DropDown

To customize default values of pager dropdown, you need to define [`pageSizes`](../api/treegrid/pageSettings/#pagesizes) as array of strings.

{% tab template="treegrid/paging", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { sampleData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, Page, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {
  
  public pageOptions: PageSettingsModel = {pageSizes: ["5", "10", "All"]};
  
  public render() {
    return (
      <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging={true} pageSettings={this.pageOptions} height={273}>
        <ColumnsDirective>
          <ColumnDirective field='taskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='taskName' headerText='Task Name' width='200'></ColumnDirective>
          <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='endDate' headerText='End Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
          <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
          <ColumnDirective field='priority' headerText='Priority' width='90' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar, Page]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}