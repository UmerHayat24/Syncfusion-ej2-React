---
title: "PDF Export"
component: "TreeGrid"
description: "Documentation on exporting TreeGrid content to PDF format and customizing the exported document with headers and footers, and file name changes."
---

# PDF Export

PDF export allows exporting TreeGrid data to PDF document. You need to use the [`pdfExport`](../api/treegrid/#pdfexport) method for exporting. To enable PDF export in the treegrid, set the [`allowPdfExport`](../api/treegrid/#allowpdfexport) as **true**.

To get start quickly with exporting functionalities, you can check on this video:
`youtube:Rz24Nk4eSEY`

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'PDF Export') {
            this.treegrid.pdfExport();
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## To customize PDF export

PDF export provides an option to customize mapping of treegrid to exported PDF document.

### File Name for Exported document

You can assign the file name for the exported document by defining `fileName` property in `PdfExportProperties`

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const exportProperties: PdfExportProperties = {
                fileName:"new.pdf"
            };
            this.treegrid.pdfExport(exportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Default Fonts for PDF exporting

By default, treegrid uses **Helvetica** font in the exported document. You can change the default font by using `PdfExportProperties.theme` property. The available default fonts are,

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
            header: {font:  new PdfStandardFont(PdfFontFamily.TimesRoman, 11, PdfFontStyle.Bold)},
            record: { font: new PdfStandardFont(PdfFontFamily.TimesRoman, 10) }
        }
    }

```

### Add Custom Font for PDF exporting

You can change the default font of TreeGrid header, content and caption cells in the exported document by using `PdfExportProperties.theme` property.

In the following example, we have used Advent Pro font to export the treegrid with Hungarian fonts.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx,app/font.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { PdfTrueTypeFont } from '@syncfusion/ej2-pdf-export';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';
import { adventProFont } from './font';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const pdfExportProperties: PdfExportProperties = {
                theme: {
                    header: {font:  new PdfTrueTypeFont(adventProFont, 12) },
                    record: { font: new PdfTrueTypeFont(adventProFont, 9) }
                }
            }
            this.treegrid.pdfExport(pdfExportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> **PdfTrueTypeFont** accepts base 64 format of the Custom Font.

### To add header and footer

You can customize text, page number, line, page size and changing orientation in header and footer.

#### How to write a text in header/footer

You can add text either in Header or Footer of exported PDF document.

```typescript

    const exportProperties: PdfExportProperties = {
        header: {
            contents: [
                {
                    position: { x: 0, y: 50 },
                    style: { textBrushColor: '#000000', fontSize: 13 },
                    type: 'Text',
                    value: "Task Details"
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
                    format: 'Page {$current} of {$total}', // optional
                    pageNumberType: 'Arabic',
                    position: { x: 0, y: 25 },
                    style: { textBrushColor: '#ffff80', fontSize: 15, hAlign: 'Center' },
                    type: 'PageNumber'
                }
            ],
            fromTop: 0,
            height: 130
        }
    }

```

#### Insert an image in header/footer

Image (Base64 string) can be added in the exported document in header/footer using the `PdfExportProperties`.

```typescript

let exportProperties: PdfExportProperties = {
    header: {
        fromTop: 0,
        height: 130,
        contents: [
            {
                type: 'Image',
                src: image,
                position: { x: 40, y: 10 },
                size: { height: 100, width: 250 },
            }
        ]
    }
}

```

The below code illustrates the pdf export customization.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx,app/image.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';
import { image } from './image';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const pdfExportProperties: PdfExportProperties = {
                footer: {
                    contents: [
                        {
                            format: 'Page {$current} of {$total}',
                            pageNumberType: 'Arabic',
                            position: { x: 0, y: 25 },
                            style: { textBrushColor: '#ffff80', fontSize: 15 },
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
              }
            this.treegrid.pdfExport(pdfExportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### How to change page orientation

Page orientation can be changed Landscape(Default Portrait) for the exported document using the `PdfExportProperties`.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const pdfExportProperties: PdfExportProperties = {
                pageOrientation: 'Landscape'
            };
            this.treegrid.pdfExport(pdfExportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### How to change page size

Page size can be customized for the exported document using the `PdfExportProperties`.

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

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const pdfExportProperties: PdfExportProperties = {
                pageSize: 'Letter'
            };
            this.treegrid.pdfExport(pdfExportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Export hidden columns

PDF export provides an option to export hidden columns of TreeGrid by defining the `includeHiddenColumn` as **true**.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const exportProperties: PdfExportProperties = {
              includeHiddenColumn: true
            };
            this.treegrid.pdfExport(exportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' visible={false} headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Show or Hide columns on Exported PDF

You can show a hidden column or hide a visible column while exporting the treegrid using [`toolbarClick`](../api/treegrid#toolbarclick) and [`pdfExportComplete`](../api/treegrid#pdfExportComplete) events.

In the [`toolbarClick`](../api/treegrid#toolbarclick) event, based on **args.item.text** as **PDF Export**. We can show or hide columns by setting [`column.visible`](../api/treegrid/column/#visible) property to **true** or **false** respectively.

In the pdfExportComplete event, We have reversed the state back to the previous state.

In the below example, we have *Duration* as a hidden column in the treegrid. While exporting, we have changed *Duration* to visible column and *StartDate* as hidden column.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { Column, ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const cols: Column[] = this.treegrid.grid.columns as Column[];
            cols[2].visible = false;
            cols[3].visible = true;
            this.treegrid.pdfExport();
        }
    }
    public pdfExportComplete(): void {
        if (this.treegrid) {
            const cols: Column[] = this.treegrid.grid.columns as Column[];
            cols[3].visible = false;
            cols[2].visible = true;
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        this.pdfExportComplete = this.pdfExportComplete.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions} pdfExportComplete={this.pdfExportComplete}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' visible={false} headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Conditional Cell Formatting

TreeGrid cells in the exported PDF can be customized or formatted using [`pdfQueryCellInfo`](../api/treegrid#pdfQueryCellInfo) event. In this event, we can format the treegrid cells of exported PDF document based on the column cell value.

In the below sample, we have set the background color for *Duration* column in the exported document by **args.cell** and *backgroundColor* property.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { Column, getObject, PdfQueryCellInfoEventArgs, QueryCellInfoEventArgs } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            this.treegrid.pdfExport();
        }
    }
    public pdfQueryCellInfo(args: PdfQueryCellInfoEventArgs): void {
        if((args.column as Column).field === 'duration'){
            if(getObject('duration', args.data) === 0) {
                args.style = {backgroundColor: '#336c12'};
            }
            else if(getObject('duration', args.data) < 3) {
                args.style = {backgroundColor: '#7b2b1d'};
            }
        }
    }
    public queryCellInfo(args: QueryCellInfoEventArgs): void {
        if ((args.column as Column).field === 'duration') {
            if (getObject('duration', args.data) === 0) {
                (args.cell as HTMLTableCellElement).style.background= '#336c12';
            } else if (getObject('duration', args.data) < 3) {
                (args.cell as HTMLTableCellElement).style.background= '#7b2b1d';
            }
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions} pdfQueryCellInfo={this.pdfQueryCellInfo} queryCellInfo={this.queryCellInfo}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Theme

PDF export provides an option to include theme for exported PDF document.

To apply theme in exported PDF, define the `theme` in `PdfExportProperties`.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const exportProperties: PdfExportProperties = {
              theme: {
                  header: {
                    bold: true,
                    border: { color: '#64FA50' },
                    fontColor: '#64FA50', fontName: 'Calibri', fontSize: 17
                  },
                  record: {
                    bold: true, fontColor: '#64FA50', fontName: 'Calibri', fontSize: 17
                  }
              }
            };
            this.treegrid.pdfExport(exportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> By default, material theme is applied to exported PDF document.

## Custom data source

PDF export provides an option to define datasource dynamically before exporting. To export data dynamically, define the `dataSource` in `PdfExportProperties`.

{% tab template="treegrid/pdfexport", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PdfExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, PdfExport, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['PdfExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            const exportProperties: PdfExportProperties = {
                 dataSource: sampleData,
            };
            this.treegrid.pdfExport(exportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowPdfExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, PdfExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}
