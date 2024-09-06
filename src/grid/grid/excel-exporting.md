---
title: "Excel Export"
component: "Grid"
description: "Documentation on exporting DataGrid content to Excel and customizing the exported document with multi-export, headers and footers, and file name changes."
---

# Excel Export

The excel export allows exporting Grid data to Excel document. You need to use the [`excelExport`](../api/grid/#excelexport) method for exporting. To enable Excel export in the grid,
 set the [`allowExcelExport`](../api/grid/#allowexcelexport) as **true**.

To use excel export, You need to inject the **ExcelExport** module in grid.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
        this.grid.excelExport();
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

## Multiple Grid exporting

The excel export provides an option to export multiple grid data in the same excel file.

### Same sheet

The excel export provides support to export multiple grids in same sheet.
To export in same sheet, define [`multipleExport.type`](../api/grid/multipleExport/#type) as **AppendToSheet** in [`ExcelExportProperties`](../api/grid/excelExportProperties/).
It have an option to provide blank rows between grids. These blank rows count can be defined by using the [`multipleExport.blankRows`](../api/grid/multipleExport/#blankrows).

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public firstGrid: Grid | null;
  public secondGrid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.firstGrid &&
        args.item.id === 'FirstGrid_excelexport') {
      const appendExcelExportProperties: ExcelExportProperties = {
        multipleExport: { type: 'AppendToSheet', blankRows: 2 }
      };
      const firstGridExport: Promise<any> = this.firstGrid.excelExport(appendExcelExportProperties, true);
      firstGridExport.then((fData: any) => {
        if (this.secondGrid) {
          this.secondGrid.excelExport(appendExcelExportProperties, false, fData);
        }
      });
    }
}
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
      <p><b>First Grid:</b></p>
      <GridComponent id='FirstGrid' dataSource={data.slice(0, 5)} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g => this.firstGrid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible={false} />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
      <p><b>Second Grid:</b></p>
      <GridComponent id='SecondGrid' dataSource={employeeData.slice(0, 5)}
        allowExcelExport={true} ref={g => this.secondGrid = g}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='120'/>
          <ColumnDirective field='LastName' headerText='Last Name' width='120'/>
          <ColumnDirective field='Title' headerText='Title' width='150'/>
        </ColumnsDirective>
        <Inject services={[ExcelExport]}/>
      </GridComponent>
  </div>
    );
  }
}
```

{% endtab %}

>By default, [`multipleExport.blankRows`](../api/grid/multipleExport/#blankrows) value is 5.

### New Sheet

Excel exporting provides support to export multiple grids in new sheet.
To export in new sheet, define  [`multipleExport.type`](../api/grid/multipleExport/#type) as **NewSheet** in [`ExcelExportProperties`](../api/grid/excelExportProperties/).

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public firstGrid: Grid | null;
  public secondGrid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.firstGrid &&
        args.item.id === 'FirstGrid_excelexport') {
      const appendExcelExportProperties: ExcelExportProperties = {
        multipleExport: { type: 'NewSheet' }
      };
      const firstGridExport: Promise<any> = this.firstGrid.excelExport(appendExcelExportProperties, true);
      firstGridExport.then((fData: any) => {
        if (this.secondGrid) {
          this.secondGrid.excelExport(appendExcelExportProperties, false, fData);
        }
      });
    }
}
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
      <p><b>First Grid:</b></p>
      <GridComponent id='FirstGrid' dataSource={data.slice(0, 5)} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g => this.firstGrid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible={false} />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
      <p><b>Second Grid:</b></p>
      <GridComponent id='SecondGrid' dataSource={employeeData.slice(0, 5)}
        allowExcelExport={true} ref={g => this.secondGrid = g}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='120'/>
          <ColumnDirective field='LastName' headerText='Last Name' width='120'/>
          <ColumnDirective field='Title' headerText='Title' width='150'/>
        </ColumnsDirective>
        <Inject services={[ExcelExport]}/>
      </GridComponent>
  </div>
    );
  }
}
```

{% endtab %}

## To customize excel export

The excel export provides an option to customize mapping of the grid to excel document.

### Export current page

The excel export provides an option to export the current page into excel. To export current page, define [`exportType`](../api/grid/excelExportProperties/#exporttype) to **CurrentPage**.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Page, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
      const excelExportProperties: ExcelExportProperties = {
          exportType: 'CurrentPage'
      };
      this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar} allowPaging={true}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, Page, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

### Export hidden columns

The excel export provides an option to export hidden columns of grid by defining [`ExcelExportProperties.includeHiddenColumn`](../api/grid/excelExportProperties/#includehiddencolumn) as **true**.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
      const excelExportProperties: ExcelExportProperties = {
        includeHiddenColumn: true
      };
      this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' visible={false}/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

### Show or Hide columns on Exported Excel

You can show a hidden column or hide a visible column while printing the grid using [`toolbarClick`](../api/grid/#toolbarclick) and [`ExcelExportComplete`](../api/grid/#excelexportcomplete) events.

In the [`toolbarClick`](../api/grid/#toolbarclick) event, based on **args.item.id** as **Grid_excelexport**. We can show or hide columns by setting [`column.visible`](../api/grid/column/#visible) property to **true** or **false** respectively.

In the excelExportComplete event, We have reversed the state back to the previous state.

In the below example, we have **CustomerID** as a hidden column in the grid. While exporting, we have changed **CustomerID** to visible column and **ShipCity** as hidden column.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Column, ExcelExport, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];

  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
        (this.grid.columns[1] as Column).visible = true;
        (this.grid.columns[3] as Column).visible = false;
        this.grid.excelExport();
    }
  }
  public excelExportComplete(): void {
    if (this.grid) {
      (this.grid.columns[1] as Column).visible = false;
      (this.grid.columns[3] as Column).visible = true;
    }
  }
  public render() {
    this.excelExportComplete = this.excelExportComplete.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}
        excelExportComplete={this.excelExportComplete}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

### Export with filter options

The excel export provides an option to export with filter option in excel by defining `enableFilter` as **true** . It requires the
[`allowFiltering`](../api/grid/#allowfiltering) to be true.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar, Filter } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
      const excelExportProperties: ExcelExportProperties = {
        enableFilter: true
      };
      this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} allowFiltering={true}
        height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' visible={false}/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport, Filter]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

### Conditional Cell Formatting

Grid cells in the exported Excel can be customized or formatted using [`excelQueryCellInfo`](../api/grid/#excelquerycellinfo) event. In this event, we can format the grid cells of exported PDF document based on the column cell value.

In the below sample, we have set the background color for **Freight** column in the exported excel by **args.style** and [`backColor`](../api/grid/excelStyle/#backcolor) property.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, ExcelQueryCellInfoEventArgs, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Column, ExcelExport, Grid, Inject, QueryCellInfoEventArgs, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];

  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
        this.grid.excelExport();
    }
  }
  public excelQueryCellInfo(args: ExcelQueryCellInfoEventArgs): void {
    if((args.column as Column).field === 'Freight'){
        if(getValue('data.Freight', args) < 30) {
            args.style = {backColor: '#99ffcc'};
        }
        else if(getValue('data.Freight', args) < 60) {
            args.style = {backColor: '#ffffb3'};
        }
        else {
            args.style = {backColor: '#ff704d'};
        }
    }
  }
  public queryCellInfo(args: QueryCellInfoEventArgs): void {
    if((args.column as Column).field === 'Freight'){
        if(getValue('data.Freight', args) < 30) {
            (args.cell as HTMLElement).style.backgroundColor = '#99ffcc';
        }
        else if(getValue('data.Freight', args) < 60) {
          (args.cell as HTMLElement).style.backgroundColor = '#ffffb3';
        }
        else {
          (args.cell as HTMLElement).style.backgroundColor = '#ff704d';
        }
    }
  }

  public render() {
    this.excelQueryCellInfo = this.excelQueryCellInfo.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    this.queryCellInfo = this.queryCellInfo.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}
        excelQueryCellInfo={this.excelQueryCellInfo} queryCellInfo={this.queryCellInfo}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

### Theme

The excel export provides an option to include theme for exported excel document.

To apply theme in exported Excel, define the [`theme`](../api/grid/excelExportProperties/#theme) in [`ExportProperties`](../api/grid/excelExportProperties/) .

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];

  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
      const excelExportProperties: ExcelExportProperties = {
          theme: {
            caption: { fontName: 'Segoe UI', fontColor: '#666666' },
            header: { fontName: 'Segoe UI', fontColor: '#666666' },
            record: { fontName: 'Segoe UI', fontColor: '#666666' }
          }
      };
      this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

>By default, material theme is applied to exported excel document.

### To add header and footer

The excel export provides an option to include header and footer content for exported excel document.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];

  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
      const excelExportProperties: ExcelExportProperties = {
        footer: {
          footerRows: 4,
          rows: [
              { cells: [{ colSpan: 4, value: "Thank you for your business!", style: { hAlign: 'Center', bold: true } }] },
              { cells: [{ colSpan: 4, value: "!Visit Again!", style: { hAlign: 'Center', bold: true } }] }
          ]
        },
        header: {
            headerRows: 7,
            rows: [
                { cells: [{ colSpan: 4, value: "Northwind Traders", style: { fontColor: '#C67878', fontSize: 20, hAlign: 'Center', bold: true, } }] },
                { cells: [{ colSpan: 4, value: "2501 Aerial Center Parkway", style: { fontColor: '#C67878', fontSize: 15, hAlign: 'Center', bold: true, } }] },
                { cells: [{ colSpan: 4, value: "Suite 200 Morrisville, NC 27560 USA", style: { fontColor: '#C67878', fontSize: 15, hAlign: 'Center', bold: true, } }] },
                { cells: [{ colSpan: 4, value: "Tel +1 888.936.8638 Fax +1 919.573.0306", style: { fontColor: '#C67878', fontSize: 15, hAlign: 'Center', bold: true, } }] },
                { cells: [{ colSpan: 4, hyperlink: { target: 'https://www.northwind.com/', displayText: 'www.northwind.com' }, style: { hAlign: 'Center' } }] },
                { cells: [{ colSpan: 4, hyperlink: { target: 'mailto:support@northwind.com' }, style: { hAlign: 'Center' } }] },
            ]
        }
      };
      this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

### File Name for Exported document

You can assign the file name for the exported document by defining `fileName` property in [`excelExportProperties`](../api/grid/excelExportProperties).

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];

  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
      const excelExportProperties: ExcelExportProperties = {
           fileName:"new.xlsx"
      };
      this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

## Custom data source

The excel export provides an option to define datasource dynamically before exporting.
To export data dynamically, define the [`dataSource`](../api/grid/excelExportProperties/#datasource) in [`ExcelExportProperties`](../api/grid/excelExportProperties/).

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];

  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
        const excelExportProperties: ExcelExportProperties = {
            dataSource: data
        };
        this.grid.excelExport(excelExportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

## Exporting grouped records

The excel export provides outline option for grouped records which hides the detailed data for better viewing.
In grid, we have provided the outline option for the exported document when the data are grouped.

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { ExcelExport, Grid, Group, GroupSettingsModel, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public groupOptions : GroupSettingsModel = {
    columns: ['CustomerID', 'ShipCity']
  };
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
        this.grid.excelExport();
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar} allowGrouping={true}
        allowExcelExport={true} toolbarClick={this.toolbarClick} ref={g=> this.grid = g} groupSettings={this.groupOptions}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' visible={false} width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, ExcelExport, Group]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

## Export the hierarchy grid

The grid have an option to export the hierarchy grid to excel document. By default, grid will exports the visible child grids in expanded state. you can change the exporting option by using the **ExcelExportProperties.hierarchyExportMode** property. The available options are,

| Mode     | Behavior    |
|----------|-------------|
| Expanded | Exports the visible child grids in expanded state. |
| All      | Exports the all the child grids in expanded state. |
| None     | Exports the child grids in collapse state. |

{% tab template="grid/excel-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, GridModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { DetailRow, ExcelExport, ExcelExportProperties, Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['ExcelExport'];
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

  public toolbarClick(args: ClickEventArgs) {
    if (this.grid && args.item.id === 'Grid_excelexport') {
      const exportProperties: ExcelExportProperties = {
          hierarchyExportMode: "Expanded"
      };
      this.grid.excelExport(exportProperties);
    }
  }

  public render(){
    this.toolbarClick = this.toolbarClick.bind(this);
    return <GridComponent ref={g => this.grid = g} id='Grid' toolbar={['ExcelExport']}
              toolbarClick={this.toolbarClick} allowExcelExport={true}
              dataSource={employeeData} childGrid={this.childGridOptions}>
              <ColumnsDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
                <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
                <ColumnDirective field='City' headerText='City' width='150'/>
                <ColumnDirective field='Country' headerText='Country' width='150'/>
            </ColumnsDirective>
            <Inject services={[DetailRow, Toolbar, ExcelExport]}/>
        </GridComponent >
  }
}
```

{% endtab %}

### Limitations

Microsoft Excel permits up to seven nested levels in outlines. So that in the grid we can able to provide only up to seven nested levels and if it exceeds more than seven levels then the document will be exported without outline option. Please refer the [Microsoft Limitation](https://docs.microsoft.com/en-us/sql/reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs?view=sql-server-2017#ExcelLimitations)

## Exporting Grid in server

The Grid have an option to export the data to Excel in server side using Grid server export library.

### Server Dependencies

The Server side export functionality is shipped in the Syncfusion.EJ2.GridExport package, which is available in Essential Studio and [nuget.org](https://www.nuget.org/).The following list of dependencies is required for Grid server side Excel exporting action.

* Syncfusion.EJ2
* Syncfusion.EJ2.GridExport

### Server Configuration

The following code snippet shows server configuration using ASP.NET Core Controller Action.

To Export the Grid in server side, You need to call the
 [`serverExcelExport`](../api/grid/#serverexcelexport) method for passing the Grid properties to server exporting action.

```typescript

        public ActionResult ExcelExport([FromForm] string gridModel)
        {
            GridExcelExport exp = new GridExcelExport();
            Grid gridProperty = ConvertGridObject(gridModel);
            return exp.ExcelExport<OrdersDetails>(gridProperty, OrdersDetails.GetAllRecords());
        }

        private Grid ConvertGridObject(string gridProperty)
        {
           Grid GridModel = (Grid)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(Grid));
           GridColumnModel cols = (GridColumnModel)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(GridColumnModel));
           GridModel.Columns = cols.columns;
           return GridModel;
        }

        public IActionResult UrlDatasource([FromBody]DataManagerRequest dm)
        {
            IEnumerable DataSource = OrdersDetails.GetAllRecords();
            DataOperations operation = new DataOperations();
            int count = DataSource.Cast<OrdersDetails>().Count();
            return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
        }


```

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public dataManager: DataManager = new DataManager({
    adaptor: new UrlAdaptor(),
    url: "Home/UrlDatasource"
  });
  public toolbar: ToolbarItems[] = ['ExcelExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_excelexport') {
        this.grid.serverExcelExport('Home/ExcelExport');
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={this.dataManager} height={270} toolbar={this.toolbar} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' format="C2" width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar]}/>
      </GridComponent>
    </div>
    );
  }
}

```

> **Note:** Refer to the GitHub sample for quick implementation and testing from [here](https://github.com/SyncfusionExamples/React-EJ2-Grid-server-side-exporting).

### CSV Export in server side

You can export the Grid to CSV format by using the [`serverCsvExport`](../api/grid/#servercsvexport) method which will pass the Grid properties to server.

In the below demo, we have invoked the above method inside the [`toolbarClick`](../api/grid/#toolbarclick) event. In server side, we have deserialized the Grid properties and passed to the `CsvExport` method which will export the properties to CSV format.

```typescript

        public ActionResult CsvGridExport([FromForm] string gridModel)
        {
            GridExcelExport exp = new GridExcelExport();
            Grid gridProperty = ConvertGridObject(gridModel);
            return exp.CsvExport<OrdersDetails>(gridProperty, OrdersDetails.GetAllRecords());
        }

        private Grid ConvertGridObject(string gridProperty)
        {
           Grid GridModel = (Grid)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(Grid));
           GridColumnModel cols = (GridColumnModel)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(GridColumnModel));
           GridModel.Columns = cols.columns;
           return GridModel;
        }

        public IActionResult UrlDatasource([FromBody]DataManagerRequest dm)
        {
            IEnumerable DataSource = OrdersDetails.GetAllRecords();
            DataOperations operation = new DataOperations();
            int count = DataSource.Cast<OrdersDetails>().Count();
            return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
        }

```

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public dataManager: DataManager = new DataManager({
    adaptor: new UrlAdaptor(),
    url: "Home/UrlDatasource"
  });
  public toolbar: ToolbarItems[] = ['CsvExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_csvexport') {
        this.grid.serverCsvExport('Home/CsvGridExport');
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={this.dataManager} height={270} toolbar={this.toolbar} toolbarClick={this.toolbarClick} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' format="C2" width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar]}/>
      </GridComponent>
    </div>
    );
  }
}

```