---
title: "Passing additional parameters to the server when Exporting"
component: "TreeGrid"
description: "Learn how to pass additional parameters to server when Exporting."
---

# Passing additional parameters to the server when Exporting

You can pass the additional parameter in the [`query`](../api/treegrid/#query) property by invoking [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method. In the [`toolbarClick`](../api/treegrid/#toolbarclick) event, you can define params as key and value pair so it will receive at the server side when exporting.

In the below example, we have passed *recordcount* as *12* using [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { Query } from '@syncfusion/ej2-data';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Toolbar, ToolbarItems, Page, TreeGrid, PdfExport, ExcelExport } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public toolbarOptions: ToolbarItems[] = ['PdfExport', 'ExcelExport'];
  public treegrid: TreeGrid | null;
  public queryClone: Query;
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.treegrid && args.item.text === 'PDF Export') {
      this.queryClone = this.treegrid.query;
      this.treegrid.query = new Query().addParams("recordcount", "12");
      this.treegrid.pdfExport();
    } else if (this.treegrid && args.item.text === 'Excel Export') {
      this.queryClone = this.treegrid.query;
      this.treegrid.query = new Query().addParams("recordcount", "12");
      this.treegrid.excelExport();
    }
  }

  public pdfExportComplete(): void {
    if (this.treegrid) {
      this.treegrid.query = this.queryClone;
    }
  }
  public excelExportComplete(): void {
    if (this.treegrid) {
      this.treegrid.query = this.queryClone;
    }
  }

  public render() {
    this.pdfExportComplete = this.pdfExportComplete.bind(this);
    this.excelExportComplete = this.excelExportComplete.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' pageSettings={this.pageOptions}
      toolbarClick={this.toolbarClick} toolbar={this.toolbarOptions} allowPaging={true}
       ref={g => this.treegrid = g} allowPdfExport={true} allowExcelExport={true}
       pdfExportComplete={this.pdfExportComplete} excelExportComplete={this.excelExportComplete}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Toolbar, Page, PdfExport, ExcelExport]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}