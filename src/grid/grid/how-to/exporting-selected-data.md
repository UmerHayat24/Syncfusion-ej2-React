---
title: "Exporting the Selected Records"
component: "Grid"
description: "Learn how to Export the Selected data."
---

# Exporting the Selected Records

You can export the selected records data by passing it to [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/) or [`ExcelExportProperties.dataSource`](../../api/grid/excelExportProperties/) property in the [`toolbarClick`](../../api/grid/#toolbarclick) event.

In the below exporting demo, we can get the selected records using [`getSelectedRecords`](../../api/grid/#getselectedrecords) method and pass the selected data to [`pdfExport`](../../api/grid/#pdfexport) or [`excelExport`](../../api/grid/#excelExport) methods using respective export properties..

 {% tab template="grid/export-filtered-data", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript

import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, PdfExportProperties } from '@syncfusion/ej2-react-grids';
import { Filter, Grid, Page, PageSettingsModel, PdfExport, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, SelectionSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public selectionOptions: SelectionSettingsModel = {type: 'Multiple'};
  public toolbar: ToolbarItems[] = ['PdfExport','ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid) {
      if (args.item.id === 'grid_pdfexport') {
        const selectedRecords = this.grid.getSelectedRecords();
        const exportProperties: PdfExportProperties = {
          dataSource: selectedRecords
        };
        this.grid.pdfExport(exportProperties);
      } else if (args.item.id === 'grid_excelexport') {
        const selectedRecords = this.grid.getSelectedRecords();
        const exportProperties: ExcelExportProperties = {
          dataSource: selectedRecords
        };
        this.grid.excelExport(exportProperties);
      }
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return <GridComponent id='grid' dataSource={data} allowPaging={true}
    allowFiltering={true} allowPdfExport={true} allowExcelExport={true} toolbar={this.toolbar}
    pageSettings={this.pageOptions} selectionSettings={this.selectionOptions} toolbarClick={this.toolbarClick}
      ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[Page, Filter,Toolbar, PdfExport, ExcelExport]} />
    </GridComponent>
  }
};
```

{% endtab %}