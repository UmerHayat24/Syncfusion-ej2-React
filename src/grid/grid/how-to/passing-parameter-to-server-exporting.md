---
title: "Passing additional parameters to the server when Exporting"
component: "Grid"
description: "Learn how to pass additional parameters to server when Exporting."
---

# Passing additional parameters to the server when Exporting

You can pass the additional parameter in the [`query`](../../api/grid/#query) property by invoking [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method. In the [`toolbarClick`](../../api/grid/#toolbarclick) event, you can define params as key and value pair so it will receive at the server side when exporting.

In the below example, we have passed *recordcount* as *12* using [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { Query } from '@syncfusion/ej2-data';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Grid, Page, PdfExport, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public queryClone: Query;
  public toolbar: ToolbarItems[] = ['PdfExport','ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid) {
      if (args.item.id === 'grid_pdfexport') {
        this.queryClone = this.grid.query;
        this.grid.query = new Query().addParams("recordcount", "12");
        this.grid.pdfExport();
      } else if (args.item.id === 'grid_excelexport') {
        this.queryClone = this.grid.query;
        this.grid.query = new Query().addParams("recordcount", "12");
        this.grid.pdfExport();
      }
    }
  }
  
  public pdfExportComplete(): void {
    if (this.grid) {
      this.grid.query = this.queryClone;
    }
  }
  public excelExportComplete(): void {
    if (this.grid) {
      this.grid.query = this.queryClone;
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    this.pdfExportComplete = this.pdfExportComplete.bind(this);
    this.excelExportComplete = this.excelExportComplete.bind(this);
    return <GridComponent id='grid' dataSource={data} allowPaging={true}
    pdfExportComplete={this.pdfExportComplete} excelExportComplete={this.excelExportComplete}
    allowFiltering={true} allowPdfExport={true} allowExcelExport={true} toolbar={this.toolbar}
    toolbarClick={this.toolbarClick}
      ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[Page, Toolbar, PdfExport, ExcelExport]} />
    </GridComponent>
  }
};
```

{% endtab %}