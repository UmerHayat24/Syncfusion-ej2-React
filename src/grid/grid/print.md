---
title: "Print"
component: "Grid"
description: "Learn how to print DataGrid content, set up pages for printing, perform external print, and print visible pages in the Essential JS 2 DataGrid control."
---

# Print

To print the Grid, use the [`print`](../api/grid/print/#print) method from grid instance.
The print option can be displayed on the [`toolbar`](../api/grid/#toolbar) by adding the **Print** toolbar item.

{% tab template="grid/print", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Toolbar} from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render(){
    return <GridComponent  dataSource={data} toolbar={['Print']} height={272}>
               <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
            </ColumnsDirective>
            <Inject services={[Toolbar]}/>
        </GridComponent >
    }
};
```

{% endtab %}

## Page Setup

Some of the print options cannot be configured through JavaScript code. So, you have to customize the layout, paper size, and margin options using the browser page setup dialog. Please refer to the following links to know more about the browser page setup:

* [`Chrome`](https://support.google.com/chrome/answer/1069693?hl=en&visit_id=1-636335333734668335-3165046395&rd=1)
* [`Firefox`](https://support.mozilla.org/en-US/kb/how-print-web-pages-firefox)
* [`Safari`](http://www.mintprintables.com/print-tips/adjust-margins-osx/)
* [`IE`](http://www.helpteaching.com/help/print/index.htm)

## Print by external button

To print the grid from an external button, invoke the [`print`](../api/grid/print/#print) method.

{% tab template="grid/print", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public clickHandler(){
    if (this.grid) {
      this.grid.print();
    }
  }
  
  public render(){
      this.clickHandler = this.clickHandler.bind(this);
      return (<div>
      <ButtonComponent onClick= { this.clickHandler }>Print</ButtonComponent>
      <GridComponent  dataSource={employeeData} height={280} ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
          <ColumnDirective field='Country' headerText='Country' width='150'/>
        </ColumnsDirective>
      </GridComponent></div>)
  }
};
```

{% endtab %}

## Print visible Page

By default, the grid prints all the pages. To print the current page alone, set the [`printMode`](../api/grid/#printmode) to **CurrentPage**.

{% tab template="grid/print", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import { Inject, Page, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public pageOptions : PageSettingsModel = { pageSize: 6 };

  public render(){
      return <GridComponent  dataSource={data} printMode='CurrentPage' toolbar={['Print']}
                allowPaging={true} pageSettings={this.pageOptions}>
                 <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Toolbar, Page]}/>
          </GridComponent >
      }
};
```

{% endtab %}

## Print the hierarchy grid

By default, the grid will be print the master and expanded child grids alone. you can change the print option by using the [`hierarchyPrintMode`](../api/grid/#hierarchyprintmode) property. The available options are,

| Mode     | Behavior    |
|----------|-------------|
| Expanded | Prints the master grid with expanded child grids. |
| All      | Prints the master grid with all the child grids. |
| None     | Prints the master grid alone. |

{% tab template="grid/print", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { DetailRow, GridModel, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public childGridOptions : GridModel = {
    columns: [
      { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
      { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
      { field: 'ShipCity', headerText: 'Ship City', width: 150 },
      { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: data,
    queryString: 'EmployeeID'
  };
  public toolbaroptions: ToolbarItems[] = ['Print'];
  public render(){
      return <GridComponent toolbar={this.toolbaroptions} hierarchyPrintMode='All' dataSource={employeeData}
                childGrid={this.childGridOptions}>
                <ColumnsDirective>
                  <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
                  <ColumnDirective field='City' headerText='City' width='150'/>
                  <ColumnDirective field='Country' headerText='Country' width='150'/>
              </ColumnsDirective>
              <Inject services={[DetailRow, Toolbar]}/>
          </GridComponent >
  }
};
```

{% endtab %}

## Print large number of columns

By default, the browser uses A4 as page size option to print pages and to adapt the size of the page the browser print preview will auto-hide the overflowed contents. Hence grid with large number of columns will cut off to adapt the print page.

To show large number of columns when printing, adjust the scale option from print option panel based on your content size.

![Scale Option Setting](./images/print-preview.png)

## Show or Hide columns while Printing

You can show a hidden column or hide a visible column while printing the grid using [`toolbarClick`](../api/grid/#toolbarclick) and [`printComplete`](../api/grid/#printcomplete) events.

In the [`toolbarClick`](../api/grid/#toolbarclick) event, based on **args.item.id** as **grid_print**. We can show or hide columns by setting [`column.visible`](../api/grid/column/#visible) property to **true** or **false** respectively.

In the printComplete event, We have reversed the state back to the previous state.

In the below example, we have **CustomerID** as a hidden column in the grid. While printing, we have changed **CustomerID** to visible column and **ShipCity** as hidden column.

{% tab template="grid/print", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { Column, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, Page, PageSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public toolbar: ToolbarItems[] = ['Print'];
  public grid: Grid | null;
  public pageOptions : PageSettingsModel = { pageSize: 6 };
  public toolbarClick(args: any): void {
    if (this.grid) {
      const cols: Column[] = this.grid.getColumns();
      for (const col of cols) {
        if (col.field === "CustomerID") {
            col.visible = true;
        }
        else if (col.field === "ShipCity") {
                col.visible = false;
        }
      }
    }
  }
  public printComplete(args: any): void {
    if (this.grid) {
      const cols: Column[] = this.grid.getColumns();
      for (const col of cols) {
        if (col.field === "CustomerID") {
          col.visible = false;
        }
        else if (col.field === "ShipCity") {
          col.visible = true;
        }
      }
    }
  }

  public render(){
    this.printComplete = this.printComplete.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return <GridComponent ref={g => this.grid = g}  dataSource={data} toolbar={this.toolbar}
              allowPaging={true} pageSettings={this.pageOptions} toolbarClick={this.toolbarClick}
              printComplete={this.printComplete}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
            <Inject services={[Toolbar, Page]}/>
        </GridComponent >
  }
};
```

{% endtab %}

## Limitations of Printing Large Data

When grid contains large number of data, printing all the data at once is not a best option for the browser performance. Because to render all the DOM elements in one page will produce performance issues in the browser. It leads to browser slow down or browser hang. Grid have option to handle large number of data by Virtualization. However while printing, it is not possible to use virtualization for rows and columns.

If printing of all the data is still needed, we suggest to Export the grid to **Excel** or **CSV** or **Pdf** and then print it from another non-web based application.
