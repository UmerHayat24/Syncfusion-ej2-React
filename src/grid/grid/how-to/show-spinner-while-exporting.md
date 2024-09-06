---
title: "Show Spinner on Grid when Exporting"
component: "Grid"
description: "Learn how to Show spinner while exporting the grid."
---

# Show Spinner on Grid when Exporting

You can show/ hide spinner component while exporting the grid using [`showSpinner`](../../api/grid/#showspinner)/ [`hideSpinner`](../../api/grid/#hidespinner) methods. You can use  [`toolbarClick`](../../api/grid/#toolbarclick) event to show spinner before exporting and hide a spinner in the [`pdfExportComplete`](../../api/grid/#pdfexportcomplete) or [`excelExportComplete`](../../api/grid/#excelexportcomplete) event after the exporting.

In the [`toolbarClick`](../../api/grid/#toolbarclick) event, based on the parameter **args.item.id** as **Grid_pdfexport** or **Grid_excelexport** we can call the [`showSpinner`](../../api/grid/#showspinner) method from grid instance.

In the [`pdfExportComplete`](../../api/grid/#pdfexportcomplete) or [`excelExportComplete`](../../api/grid/#excelexportcomplete) event, We can call the [`hideSpinner`](../../api/grid/#hidespinner) method.

In the below demo, we have rendered the default spinner component when exporting the grid.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, ExcelExport, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Grid, Page, PageSettingsModel, PdfExport, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public toolbar: ToolbarItems[] = ['PdfExport','ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid) {
      if (args.item.id === 'grid_pdfexport') {
        this.grid.showSpinner();
        this.grid.pdfExport();
      }
      else if (args.item.id === 'grid_excelexport') {
          this.grid.showSpinner();
          this.grid.pdfExport();
      }
    }
  }
  public pdfExportComplete(): void {
    if (this.grid) {
      this.grid.hideSpinner();
    }
  }
  public excelExportComplete(): void {
    if (this.grid) {
      this.grid.hideSpinner();
    }
  }
  public render() {
    this.pdfExportComplete = this.pdfExportComplete.bind(this);
    this.excelExportComplete = this.excelExportComplete.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return <GridComponent id='grid' dataSource={data} allowPaging={true} allowPdfExport={true}
    pdfExportComplete={this.pdfExportComplete} excelExportComplete={this.excelExportComplete}
    allowExcelExport={true} toolbar={this.toolbar} pageSettings={this.pageOptions} toolbarClick={this.toolbarClick}
      ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[Page, Toolbar, ExcelExport, PdfExport]} />
    </GridComponent>
  }
};
```

{% endtab %}