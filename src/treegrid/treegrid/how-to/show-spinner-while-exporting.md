---
title: "Show Spinner on TreeGrid when Exporting"
component: "TreeGrid"
description: "Learn how to Show spinner while exporting the treegrid."
---

# Show Spinner on TreeGrid when Exporting

You can show/ hide spinner component while exporting the treegrid using [`showSpinner`](../api/treegrid/#showspinner)/ [`hideSpinner`](../api/treegrid/#hidespinner) methods. You can use  [`toolbarClick`](../api/treegrid/#toolbarclick) event to show spinner before exporting and hide a spinner in the [`pdfExportComplete`](../api/treegrid/#pdfexportcomplete) or [`excelExportComplete`](../api/treegrid/#excelexportcomplete) event after the exporting.

In the [`toolbarClick`](../../api/grid/#toolbarclick) event, based on the parameter **args.item.text** as **PDF Export** or **Excel Export** we can call the [`showSpinner`](../api/treegrid/#showspinner) method from grid instance.

In the [`pdfExportComplete`](../api/treegrid/#pdfexportcomplete) or [`excelExportComplete`](../api/treegrid/#excelexportcomplete) event, We can call the [`hideSpinner`](../api/treegrid/#hidespinner) method.

In the below demo, we have rendered the default spinner component when exporting the treegrid.

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Toolbar, ToolbarItems, Page, TreeGrid, PdfExport, ExcelExport } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public toolbarOptions: ToolbarItems[] = ['PdfExport', 'ExcelExport'];
  public treegrid: TreeGrid | null;
  public selectionOptions: SelectionSettingsModel = {type: 'Multiple'};
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.treegrid && args.item.text === 'PDF Export') {
      this.treegrid.showSpinner();
      this.treegrid.pdfExport();
    } else if (this.treegrid && args.item.text === 'Excel Export') {
        this.treegrid.showSpinner();
        this.treegrid.excelExport();
    }
  }

  public pdfExportComplete(): void {
    if (this.treegrid) {
      this.treegrid.hideSpinner();
    }
  }
  public excelExportComplete(): void {
    if (this.treegrid) {
      this.treegrid.hideSpinner();
    }
  }

  public render() {
    this.pdfExportComplete = this.pdfExportComplete.bind(this);
    this.excelExportComplete = this.excelExportComplete.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' allowPaging={true} pageSettings={this.pageOptions}
      toolbarClick={this.toolbarClick} toolbar={this.toolbarOptions} allowPaging={true}
       ref={g => this.treegrid = g} allowPdfExport={true} allowExcelExport={true}
       selectionSettings={this.selectionOptions} pdfExportComplete={this.pdfExportComplete} excelExportComplete={this.excelExportComplete}>
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
