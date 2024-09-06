---
title: "Exporting Filtered Data Only"
component: "TreeGrid"
description: "Learn how to customize the Essential JS 2 TreeGrid."
---

# Exporting Filtered Data Only

You can export the filtered data by defining the resulted data in [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/#datasource) before export.

In the below Pdf exporting demo, We have gotten the filtered data from the filteredResult of TreeGrid filterModule and then defines the resulted data in [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/#datasource) and pass it to [`pdfExport`](../api/treegrid/#pdfexport) method.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { PdfExportProperties } from '@syncfusion/ej2-react-grids';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Filter, Toolbar, ToolbarItems, Page, TreeGrid, PdfExport } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public toolbarOptions: ToolbarItems[] = ['PdfExport'];
  public treegrid: TreeGrid | null;
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.treegrid && args.item.text === 'PDF Export') {
         // get all filtered records
          let pdfdata: object[] = [];
          pdfdata = this.treegrid.filterModule.filteredResult;
          const exportProperties: PdfExportProperties = {
            dataSource: pdfdata,
          };
          if (this.treegrid) {
            this.treegrid.pdfExport(exportProperties);
          }
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' pageSettings={this.pageOptions}
      toolbarClick={this.toolbarClick} toolbar={this.toolbarOptions} allowPaging={true}
       ref={g => this.treegrid = g} allowFiltering={true} allowPdfExport={true}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Filter, Toolbar, Page, PdfExport]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}
