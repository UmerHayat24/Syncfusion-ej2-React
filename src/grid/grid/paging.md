---
title: "Paging"
component: "Grid"
description: "Learn how to add custom elements in Pager using pager template and customize the pager in the Essential JS 2 DataGrid control."
---

# Paging

Paging provides an option to display Grid data in page segments.
To enable paging, set the [`allowPaging`](../api/grid/#allowpaging) to true.
When paging is enabled, pager component renders at the bottom of the grid.
Paging options can be configured through the [`pageSettings`](../api/grid/pageSettings/).

In the below sample, [`pageSize`](../api/grid/pageSettings/#pagesize) is calculated based on the grid height by using the [`load`](../api/grid/#load) event.

To use Paging, inject **Page** module in Grid.

{% tab template="grid/pager", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Grid, GridComponent, Inject, Page } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private gridInstance: Grid | null;
  public onLoad() {
    if (this.gridInstance) {
      /** height of the each row */
      const rowHeight: number = this.gridInstance.getRowHeight();
      /** Grid height */
      const gridHeight: number = this.gridInstance.height as number;
      /** initial page size */
      const pageSize: number = this.gridInstance.pageSettings.pageSize as number;
      /** new page size is obtained here */
      const pageResize: any = (gridHeight - (pageSize * rowHeight)) / rowHeight;
      this.gridInstance.pageSettings.pageSize = pageSize + Math.round(pageResize);
    }
  }

  public render(){
      this.onLoad = this.onLoad.bind(this);
      return <GridComponent  dataSource={data} ref={grid => this.gridInstance = grid} allowPaging={true} height={325} load={this.onLoad}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page]}/>
          </GridComponent>
      }
};
```

{% endtab %}

> Grid Paging enables you to achieve better performance by fetching only a predefined number of records from the data source.

## Template

You can use custom elements inside the pager instead of default elements. The custom elements can be defined by using the [`template`](../api/grid/pageSettings/#template) property. Inside this template, you can access the [`currentPage`](../api/grid/pageSettings/#currentpage), [`pageSize`](../api/grid/pageSettings/#pagesize), [`pageCount`](../api/grid/pageSettings/#pagecount), totalPage and totalRecordsCount values.

{% tab template="grid/pager", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { NumericTextBoxComponent } from "@syncfusion/ej2-react-inputs";
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { GridComponent, Inject, Grid, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public change(args) {
         this.grid.pageSettings.currentPage = args.value;
  }
  public template(pagerData) {
    return (
      <div className="e-pagertemplate">
        <div className="col-lg-12 control-section">
            <div className="content-wrapper">
            <NumericTextBoxComponent min={1} max={3} value={pagerData.currentPage} format='###.##' change={this.change.bind(this)}></NumericTextBoxComponent>
          </div>
        </div>
        <div
          id="totalPages"
          className="e-pagertemplatemessage" style={{ marginTop: 8, marginLeft: 30, border: "none", display: "inline-block"}}>
          <span className="e-pagenomsg">
            {pagerData.currentPage} of {pagerData.totalPages} pages ({pagerData.totalRecordsCount} items)
          </span>
        </div>
      </div>
    );
  }
  public render(){
      return <GridComponent  dataSource={data} allowPaging={true} pageSettings={{ template: this.template.bind(this), pageSize: 5 }} ref={g=> this.grid = g}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='100'/>
              </ColumnsDirective>
              <Inject services={[Page]}/>
          </GridComponent>
  }
};
```

{% endtab %}

## Pager with Page Size Dropdown

The pager Dropdown allows you to change the number of records in the Grid dynamically. It can be enabled by defining the [`pageSettings.pageSizes`](../api/grid/pageSettings/#pagesizes) property as **true**.

{% tab template="grid/pager", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { GridComponent, Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public pageOptions: PageSettingsModel = {
    pageSize: 8, pageSizes: true
  };
  public render(){
      return <GridComponent  dataSource={data} allowPaging={true} height={268} pageSettings={this.pageOptions}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='100'/>
              </ColumnsDirective>
              <Inject services={[Page]}/>
          </GridComponent>
  }
};
```

{% endtab %}

## How to render Pager at the Top of the Grid

By default, Pager will be rendered at the bottom of the Grid. You can also render the Pager at the top of the Grid by using the [`dataBound`](../api/grid/#databound) event.

{% tab template="grid/pager", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, GridComponent, Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public gridInstance: Grid | null;
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  public initialGridLoad: boolean = true;
  public pageOptions: PageSettingsModel = {
    pageSize: 8, pageSizes: true
  };
  public dataBound() {
      if (this.initialGridLoad && this.gridInstance) {
          this.initialGridLoad = false;
          const pager: any = document.getElementsByClassName('e-gridpager');
          let topElement: any;
          if (this.gridInstance.allowGrouping || this.gridInstance.toolbar) {
              topElement = this.gridInstance.allowGrouping ? document.getElementsByClassName('e-groupdroparea') :
                          document.getElementsByClassName('e-toolbar');
          } else {
              topElement = document.getElementsByClassName('e-gridheader');
          }
          this.gridInstance.element.insertBefore(pager[0], topElement[0]);
      }
  }
  public render(){
      this.dataBound = this.dataBound.bind(this);
      return <GridComponent  dataSource={data} ref={grid => this.gridInstance = grid}
                toolbar={this.toolbarOptions} allowPaging={true} height={268}
                pageSettings={this.pageOptions} dataBound={this.dataBound}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page, Toolbar]}/>
          </GridComponent>
  }
};
```

{% endtab %}

> During the paging action, the pager component triggers the below three events.
> * The [`created`](https://ej2.syncfusion.com/react/documentation/api/pager/#created) event triggers when Pager is created.
> * The [`click`](https://ej2.syncfusion.com/react/documentation/api/pager/#click) event triggers when the numeric items in the pager is clicked.
> * The [`dropDownChanged`](https://ej2.syncfusion.com/react/documentation/api/pager/#dropdownchanged) event triggers when pageSize DropDownList value is selected.

## See Also

[Group with Paging](./grouping#group-with-paging)
