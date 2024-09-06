---
title: "Customizing Filter Dialog by using additional Parameter"
component: "TreeGrid"
description: "Learn how to customize the filter dialog in TreeGrid by using an additional Parameter."
---

# Customizing Filter Dialog by using an additional Parameter

You can customize the default settings of the components which are used in Menu filter by using params of filter property in column definition.
In the below sample, TaskID and Duration Columns are numeric columns, while open the filter dialog then you can see that NumericTextBox with spin button is displayed to change/set the filter value. Now using the params option we hide the spin button in NumericTextBox for TaskID Column.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Page, TreeGrid, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { IFilter } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public treegrid: TreeGrid | null;

  public FilterOptions: FilterSettingsModel = {
    type: 'Menu'
  };
  
  public ifilter: IFilter = { params: {showSpinButton: false}};

  public render() {
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' allowFiltering={true}  filterSettings={this.FilterOptions}
      ref={g => this.treegrid = g} height={273}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' filter={this.ifilter} textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Filter, Page]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}