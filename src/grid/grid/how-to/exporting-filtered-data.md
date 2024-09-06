---
title: "Exporting Filtered Data Only"
component: "Grid"
description: "Learn how to Exporting Filtered Data Only."
---

# Exporting Filtered Data Only

You can export the filtered data by defining the resulted data in [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/#datasource) before export.

In the below Pdf exporting demo, We have gotten the filtered data by applying filter query to the grid data and then defines the resulted data in [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/#datasource) and pass it to [`pdfExport`](../../api/grid/#pdfexport) method.

 {% tab template="grid/export-filtered-data", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, PdfExportProperties } from '@syncfusion/ej2-react-grids';
import { Filter, Grid, Page, PageSettingsModel, PdfExport, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      let pdfdata: object[] = [];
      const query = this.grid.renderModule.data.generateQuery(); // get grid corresponding query
      for(let i=0; i<query.queries.length; i++ ){
        if(query.queries[i].fn === 'onPage'){
          query.queries.splice(i,1);// remove page query to get all records
          break;
        }
      }
      new DataManager({ json: data}).executeQuery(query)
        .then((e: any) => {
          pdfdata = e.result;   // get all filtered records
          const exportProperties: PdfExportProperties = {
            dataSource: pdfdata,
          };
          if (this.grid) {
            this.grid.pdfExport(exportProperties);
          }
      }).catch((e) => true);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return <GridComponent id='grid' dataSource={data} allowPaging={true}
      allowFiltering={true} allowPdfExport={true} toolbar={this.toolbar}
      pageSettings={this.pageOptions} toolbarClick={this.toolbarClick}
      ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[Page, Filter,Toolbar, PdfExport]} />
    </GridComponent>
  }
};
```

{% endtab %}
