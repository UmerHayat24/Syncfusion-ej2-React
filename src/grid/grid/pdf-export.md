---
title: "PDF Export"
component: "Grid"
description: "Documentation on exporting DataGrid content to PDF format and customizing the exported document with multi-export, headers and footers, and file name changes."
---

# PDF Export

PDF export allows exporting Grid data to PDF document. You need to use the [`pdfExport`](../api/grid/#pdfexport) method for exporting. To enable PDF export in the grid, set the [`allowPdfExport`](../api/grid/#allowpdfexport) as **true**.

To use PDF export, inject the **PdfExport** module in grid.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
    public grid: Grid | null;
    public toolbar: ToolbarItems[] = ['PdfExport'];
    public toolbarClick = (args: ClickEventArgs) => {
        if (this.grid && args.item.id === 'grid_pdfexport') {
            this.grid.pdfExport();
        }
    }
    public render() {
      this.toolbarClick = this.toolbarClick.bind(this);
      return (
        <div>
          <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar} allowPdfExport={true}
            allowPaging={true} toolbarClick={this.toolbarClick } ref={g=> this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
                <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible={false}/>
            </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
        </div>
      );
    }
}
```

{% endtab %}

## Multiple exporting

PDF export provides an option for exporting multiple grids to same file.
In this exported document, each grid will be exported to new page of document in same file.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {

  public toolbar: ToolbarItems[] = ['PdfExport'];
  public firstGrid: Grid | null;
  public secondGrid:  Grid | null;
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.firstGrid && args.item.id === 'FirstGrid_pdfexport') {
      const firstGridPdfExport: Promise<object> = this.firstGrid.pdfExport({}, true);
      firstGridPdfExport.then((pdfData: object) => {
        if (this.secondGrid) {
          this.secondGrid.pdfExport({}, false, pdfData);
        }
      });
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
          <div><b>First Grid:</b></div>
          <GridComponent id='FirstGrid' dataSource={data.slice(0, 5)} toolbar={this.toolbar}
              allowPdfExport={true} toolbarClick={this.toolbarClick}
              ref={g => this.firstGrid = g}>
              <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
                  <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
                  <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible={false} />
              </ColumnsDirective>
              <Inject services={[Toolbar, PdfExport]}/>
          </GridComponent>
          <div><b>Second Grid:</b></div>
          <GridComponent id='SecondGrid' dataSource={employeeData.slice(0, 5)} allowPdfExport={true}
              ref={g => this.secondGrid = g}>
              <ColumnsDirective>
                  <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='FirstName' headerText='First Name' width='120'/>
                  <ColumnDirective field='LastName' headerText='Last Name' width='120'/>
                  <ColumnDirective field='Title' headerText='Title' width='150'/>
              </ColumnsDirective>
              <Inject services={[PdfExport]}/>
          </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

## To customize PDF export

PDF export provides an option to customize mapping of grid to exported PDF document.

### File Name for Exported document

You can assign the file name for the exported document by defining [`fileName`](../api/grid/pdfExportProperties/#filename) property in [`PdfExportProperties`](../api/grid/pdfExportProperties/).

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {

  public toolbar: ToolbarItems[] = ['PdfExport'];
  public grid: Grid | null;
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
        const exportProperties: PdfExportProperties = {
             fileName:'new.pdf'
        };
        this.grid.pdfExport(exportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
          <GridComponent id='grid' dataSource={data.slice(0, 5)} toolbar={this.toolbar}
              allowPdfExport={true} toolbarClick={this.toolbarClick}
              ref={g => this.grid = g}>
              <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
                  <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
                  <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
              </ColumnsDirective>
              <Inject services={[Toolbar, PdfExport]}/>
          </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### Default Fonts for PDF exporting

By default, grid uses **Helvetica** font in the exported document. You can change the default font by using [`PdfExportProperties.theme`](../api/grid/pdfExportProperties/#theme) property. The available default fonts are,

* Helvetica
* TimesRoman
* Courier
* Symbol
* ZapfDingbats

The code example for changing default font,

```typescript

    import { PdfFontFamily, PdfFontStyle, PdfStandardFont } from '@syncfusion/ej2-pdf-export';

    ...

    const pdfExportProperties: PdfExportProperties = {
      theme: {
        caption: { font: new PdfStandardFont(PdfFontFamily.TimesRoman, 9) },
        header: { font:  new PdfStandardFont(PdfFontFamily.TimesRoman, 11, PdfFontStyle.Bold) },
        record: { font: new PdfStandardFont(PdfFontFamily.TimesRoman, 10) }
      }
    };

```

### Add Custom Font for PDF exporting

You can change the default font of Grid header, content and caption cells in the exported document by using [`PdfExportProperties.theme`](../api/grid/pdfExportProperties/#theme) property.

In the following example, we have used Algeria font to export the grid.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/font.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { PdfTrueTypeFont } from '@syncfusion/ej2-pdf-export';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';
import { adventProFont } from './font';

export default class App extends React.Component<{}, {}> {

  public toolbar: ToolbarItems[] = ['PdfExport'];
  public grid: Grid | null;
  public toolbarClick = (args: ClickEventArgs) => {
    const pdfExportProperties: PdfExportProperties = {
      theme: {
          caption: { font: new PdfTrueTypeFont(adventProFont, 10) },
          header: {font:  new PdfTrueTypeFont(adventProFont, 12) },
          record: { font: new PdfTrueTypeFont(adventProFont, 9) }
      }
    };
    if (this.grid) {
      this.grid.pdfExport(pdfExportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
          <GridComponent id='grid' dataSource={data.slice(0, 5)} toolbar={this.toolbar}
              allowPdfExport={true} toolbarClick={this.toolbarClick}
              ref={g => this.grid = g}>
              <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
                  <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
                  <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
              </ColumnsDirective>
              <Inject services={[Toolbar, PdfExport]}/>
          </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

> **PdfTrueTypeFont** accepts base 64 format of the Custom Font.

### To add header and footer

You can customize text, page number, line, page size and changing orientation in header and footer.

#### How to write a text in header/footer

You can add text either in Header or Footer of exported PDF document using [`pdfExportProperties`](../api/grid/#pdfexportproperties).

```typescript

    const exportProperties: PdfExportProperties = {
      header: {
        contents: [
            {
                position: { x: 0, y: 50 },
                style: { textBrushColor: '#000000', fontSize: 13 },
                type: 'Text',
                value: "Northwind Traders"
            }
        ],
        fromTop: 0,
        height: 130
      }
    }

```

#### How to draw a line in header/footer

you can add line either in Header or Footer of the exported PDF document.

Supported line styles:
* dash
* dot
* dashdot
* dashdotdot
* solid

```typescript

    const exportProperties: PdfExportProperties = {
      header: {
        contents: [
            {
                type: 'Line',
                style: { penColor: '#000080', penSize: 2, dashStyle: 'Solid' },
                points: { x1: 0, y1: 4, x2: 685, y2: 4 }
            }
        ],
        fromTop: 0,
        height: 130
      }
    }

```

#### Add page number in header/footer

you can add page number either in Header or Footer of exported PDF document.

Supported page number types:
* LowerLatin - a, b, c,
* UpperLatin - A, B, C,
* LowerRoman - i, ii, iii,
* UpperRoman - I, II, III,
* Number - 1,2,3.

```typescript

const exportProperties: PdfExportProperties = {
      header: {
        contents: [
            {
              /** format is optional */
              format: 'Page {$current} of {$total}',
              pageNumberType: 'Arabic',
              position: { x: 0, y: 25 },
              style: {
                fontSize: 15,
                hAlign: 'Center',
                textBrushColor: '#ffff80',
              },
              type: 'PageNumber',
            }
        ],
        fromTop: 0,
        height: 130
    }
  }

```

#### Insert an image in header/footer

Image (Base64 string) can be added in the exported document in header/footer using the [`PdfExportProperties`](../api/grid/pdfExportProperties/).

```typescript

    let exportProperties: PdfExportProperties = {
      header: {
        contents: [
            {
              position: { x: 40, y: 10 },
              size: { height: 100, width: 250 },
              src: image,
              type: 'Image'
            }
        ],
        fromTop: 0,
        height: 130
      }
    }

```

The below code illustrates the pdf export customization.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/image.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';
import { image } from './image';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (args.item.id === 'grid_pdfexport') {
      const pdfExportProperties: PdfExportProperties = {
        footer: {
          contents: [
              {
                format: 'Page {$current} of {$total}',
                pageNumberType: 'Arabic',
                position: { x: 0, y: 25 },
                style: {
                  fontSize: 15,
                  textBrushColor: '#ffff80'
                },
                type: 'PageNumber'
              }
          ],
          fromBottom: 160,
          height: 150
        },
        header: {
          contents: [
              {
                position: { x: 40, y: 10 },
                size: { height: 100, width: 250 },
                src: image,
                type: 'Image'
              }
          ],
          fromTop: 0,
          height: 130
        }
      };
      if (this.grid) {
        this.grid.pdfExport(pdfExportProperties);
      }
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
              <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
              <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
              <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### How to change page orientation

Page orientation can be changed Landscape(Default Portrait) for the exported document using the [`PdfExportProperties.pageOrientation`](../api/grid/pdfExportProperties/#pageorientation).

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
          pageOrientation: 'Landscape',
      };
      this.grid.pdfExport(exportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
              <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
              <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
              <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### How to change page size

Page size can be customized for the exported document using the [`PdfExportProperties.pageSize`](../api/grid/pdfExportProperties/#pagesize).
Supported page sizes are:
* Letter
* Note
* Legal
* A0
* A1
* A2
* A3
* A5
* A6
* A7
* A8
* A9
* B0
* B1
* B2
* B3
* B4
* B5
* Archa
* Archb
* Archc
* Archd
* Arche
* Flsa
* HalfLetter
* Letter11x17
* Ledger

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
        pageSize: 'Letter'
      };
      this.grid.pdfExport(exportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
              <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
              <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
              <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### Export current page

PDF export provides an option to export the current page into PDF. To export current page, define the [`PdfExportProperties.exportType`](../api/grid/pdfExportProperties/#exporttype) to **CurrentPage**.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, Page, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
        exportType: 'CurrentPage'
      };
      this.grid.pdfExport(exportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g} allowPaging={true}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
              <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
              <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
              <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport, Page]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### Export hidden columns

PDF export provides an option to export hidden columns of Grid by defining the [`PdfExportProperties.includeHiddenColumn`](../api/grid/pdfExportProperties/#includehiddencolumn) as **true**.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
        includeHiddenColumn: true
      };
      this.grid.pdfExport(exportProperties);
    }
  }

  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g} >
          <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible={false}/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### Show or Hide columns on Exported PDF

You can show a hidden column or hide a visible column while exporting the grid using [`toolbarClick`](../api/grid/#toolbarclick) and [`pdfExportComplete`](../api/grid/#pdfexportcomplete) events.

In the [`toolbarClick`](../api/grid/#toolbarclick) event, based on **args.item.id** as **Grid_pdfexport**. We can show or hide columns by setting [`column.visible`](../api/grid/column/#visible) property to **true** or **false** respectively.

In the pdfExportComplete event, We have reversed the state back to the previous state.

In the below example, we have **CustomerID** as a hidden column in the grid. While exporting, we have changed **CustomerID** to visible column and **ShipCity** as hidden column.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Column, Grid, Inject, PdfExport, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      (this.grid.columns[1] as Column).visible = true;
      (this.grid.columns[3] as Column).visible = false;
      this.grid.pdfExport();
    }
  }
  public pdfExportComplete(): void {
    if (this.grid) {
      (this.grid.columns[1] as Column).visible = false;
      (this.grid.columns[3] as Column).visible = true;
    }
  }
  public render() {
    this.pdfExportComplete = this.pdfExportComplete.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} pdfExportComplete={this.pdfExportComplete} ref={g => this.grid = g} >
          <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
            <ColumnDirective field='CustomerID' visible={false} headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' visible={false} headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### Conditional Cell Formatting

Grid cells in the exported PDF can be customized or formatted using [`pdfQueryCellInfo`](../api/grid/pdfQueryCellInfoEventArgs/#cell) event. In this event, we can format the grid cells of exported PDF document based on the column cell value.

In the below sample, we have set the background color for **Freight** column in the exported document by **args.cell** and **backgroundColor** property.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Column, Grid, Inject, PdfExport, PdfQueryCellInfoEventArgs, QueryCellInfoEventArgs, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
        this.grid.pdfExport();
    }
  }
  public pdfQueryCellInfo(args: PdfQueryCellInfoEventArgs): void {
    if((args.column as Column).field === 'Freight'){
        if(getValue('data.Freight', args) < 30) {
            args.style = {backgroundColor: '#99ffcc'};
        }
        else if(getValue('data.Freight', args) < 60) {
            args.style = {backgroundColor: '#ffffb3'};
        }
        else {
            args.style = {backgroundColor: '#ff704d'};
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
    this.queryCellInfo = this.queryCellInfo.bind(this);
    this.pdfQueryCellInfo = this.pdfQueryCellInfo.bind(this);
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} pdfQueryCellInfo={this.pdfQueryCellInfo}
          queryCellInfo={this.queryCellInfo} ref={g => this.grid = g} >
          <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
            <ColumnDirective field='CustomerID' visible={false} headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' visible={false} headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

### Theme

PDF export provides an option to include theme for exported PDF document.

To apply theme in exported PDF, define the [`theme`](../api/grid/pdfExportProperties/#theme) in [`exportProperties`](../api/grid/pdfExportProperties/) .

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
          theme: {
            caption: {
              bold: true,
              fontColor: '#64FA50',
              fontName: 'Calibri',
              fontSize: 17
            },
            header: {
              bold: true,
              border: { color: '#64FA50' },
              fontColor: '#64FA50',
              fontName: 'Calibri',
              fontSize: 17
            },
            record: {
              bold: true,
              fontColor: '#64FA50',
              fontName: 'Calibri',
              fontSize: 17
            }
          }
      };
      if (this.grid) {
        this.grid.pdfExport(exportProperties);
      }
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g} >
          <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

> By default, material theme is applied to exported PDF document.

## Custom data source

PDF export provides an option to define datasource dynamically before exporting. To export data dynamically, define the [`dataSource`](../api/grid/pdfExportProperties/#datasource) in [`PdfExportProperties`](../api/grid/pdfExportProperties/)

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
          dataSource: data
      };
      this.grid.pdfExport(exportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g}>
          <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right' />
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
            <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
          </ColumnsDirective>
          <Inject services={[Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

## Export the hierarchy grid

The grid have an option to export the hierarchy grid to pdf document. By default, grid will exports the master grid with expanded child grids alone. you can change the exporting option by using the **PdfExportProperties.hierarchyExportMode** property. The available options are,

| Mode     | Behavior    |
|----------|-------------|
| Expanded | Exports the master grid with expanded child grids. |
| All      | Exports the master grid with all the child grids. |
| None     | Exports the master grid alone. |

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, DetailRow, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, GridModel, Inject, PdfExport, PdfExportProperties, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  
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
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      const exportProperties: PdfExportProperties = {
          hierarchyExportMode: "Expanded"
      };
      this.grid.pdfExport(exportProperties);
    }
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={employeeData} toolbar={this.toolbar} allowPdfExport={true}
          toolbarClick={this.toolbarClick} ref={g => this.grid = g} childGrid={this.childGridOptions}>
          <ColumnsDirective>
            <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
            <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
            <ColumnDirective field='City' headerText='City' width='150'/>
            <ColumnDirective field='Country' headerText='Country' width='150'/>
          </ColumnsDirective>
          <Inject services={[DetailRow, Toolbar, PdfExport]}/>
        </GridComponent>
      </div>
    );
  }
}
```

{% endtab %}

> By default, the hierarchy grid exports the expanded child grids from the visible page only. Refer [Export the expanded state of hierarchy grid from other pages](./how-to#export-the-expanded-state-of-hierarchy-grid-from-other-pages).

## Repeat column header on every page

By default, column header will be placed on the first page of the pdf document but you can display column header on every page using **repeatHeader** property of **pdfGrid**.

In the below sample, we have enabled **repeatHeader** property in [`pdfHeaderQueryCellInfo`](../api/grid/#pdfheaderquerycellinfo) event to show the header on every page.

{% tab template="grid/pdf-export", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, GridComponent, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, PdfExport, PdfHeaderQueryCellInfoEventArgs, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
      this.grid.pdfExport();
    }
  }
  public pdfHeaderQueryCellInfo(args: PdfHeaderQueryCellInfoEventArgs): void {
     (args.cell as any).row.pdfGrid.repeatHeader = true;
  }
  public render() {
    this.toolbarClick = this.toolbarClick.bind(this);
    return (
      <div>
        <GridComponent id='grid' dataSource={data} height={270} toolbar={this.toolbar}
        allowPdfExport={true} toolbarClick={this.toolbarClick}
        pdfHeaderQueryCellInfo={this.pdfHeaderQueryCellInfo} ref={g=> this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' />
            <ColumnDirective field='Freight' width='100' textAlign='Right'/>
            <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
            <ColumnDirective field='ShipName' headerText='Ship Name' width='150' />
        </ColumnsDirective>
        <Inject services={[Toolbar, PdfExport]}/>
      </GridComponent>
    </div>
    );
  }
}
```

{% endtab %}

## Exporting Grid in server

The Grid have an option to export the data to PDF in server side using Grid server export library.

### Server Dependencies

The Server side export functionality is shipped in the Syncfusion.EJ2.GridExport package, which is available in Essential Studio and [nuget.org](https://www.nuget.org/).The following list of dependencies is required for Grid server side PDF exporting action.

* Syncfusion.EJ2
* Syncfusion.EJ2.GridExport

### Server Configuration

The following code snippet shows server configuration using ASP.NET Core Controller Action.

To Export the Grid in server side, You need to call the
 [`serverPdfExport`](../api/grid/#serverpdfexport) method for passing the Grid properties to server exporting action.

```typescript

        public ActionResult PdfExport([FromForm] string gridModel)
        {
            GridPdfExport exp = new GridPdfExport();
            Grid gridProperty = ConvertGridObject(gridModel);
            return exp.PdfExport<OrdersDetails>(gridProperty, OrdersDetails.GetAllRecords());
        }

        private Grid ConvertGridObject(string gridProperty)
        {
           Grid GridModel = (Grid)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(Grid));
           GridColumnModel cols = (GridColumnModel)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(GridColumnModel));
           GridModel.Columns = cols.columns;
           return GridModel;
        }

        public class GridColumnModel
        {
            public List<GridColumn> columns { get; set; }
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
  public toolbar: ToolbarItems[] = ['PdfExport'];
  public toolbarClick = (args: ClickEventArgs) => {
    if (this.grid && args.item.id === 'grid_pdfexport') {
        this.grid.serverPdfExport('Home/PdfExport');
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

## See Also

* [How to export the Grid when using non english font in React Grid](https://www.syncfusion.com/forums/148193/how-to-export-the-grid-when-using-non-english-font-in-react-grid)