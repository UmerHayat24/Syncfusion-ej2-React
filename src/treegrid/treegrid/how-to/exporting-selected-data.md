---
title: "Exporting the Selected Records"
component: "TreeGrid"
description: "Learn how to Export the Selected data."
---

# Exporting the Selected Records

You can export the selected records data by passing it to [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/) or [`ExcelExportProperties.dataSource`](../../api/grid/excelExportProperties/) property in the [`toolbarClick`](../../api/grid/#toolbarclick) event.

In the below exporting demo, we can get the selected records using [`getSelectedRecords`](../api/treegrid/#getselectedrecords) method and pass the selected data to [`pdfExport`](../api/treegrid/#pdfexport) or [`excelExport`](../api/treegrid/#excelExport) methods using respective export properties..

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { PdfExportProperties, ExcelExportProperties } from '@syncfusion/ej2-react-grids';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Toolbar, ToolbarItems, Page, TreeGrid, PdfExport, ExcelExport } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public toolbarOptions: ToolbarItems[] = ['PdfExport', 'ExcelExport'];
  public treegrid: TreeGrid | null;
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public selectionOptions: SelectionSettingsModel = {type: 'Multiple'};
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.treegrid && args.item.text === 'PDF Export') {
      const selectedRecords = this.treegrid.getSelectedRecords();
      const exportProperties: PdfExportProperties = {
        dataSource: selectedRecords,
      };
      this.treegrid.pdfExport(exportProperties);
    } else if (this.treegrid && args.item.text === 'Excel Export') {
      const selectedRecords = this.treegrid.getSelectedRecords();
      const exportProperties: ExcelExportProperties = {
        dataSource: selectedRecords,
      };
      this.treegrid.excelExport(exportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' pageSettings={this.pageOptions}
      toolbarClick={this.toolbarClick} toolbar={this.toolbarOptions} allowPaging={true}
       ref={g => this.treegrid = g} allowPdfExport={true} allowExcelExport={true}
       selectionSettings={this.selectionOptions}>
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
