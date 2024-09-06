---
title: "Migration"
component: "TreeGrid"
description: "Documentation on exporting TreeGrid content to Excel document and customizing the exported document with headers and footers, and file name changes."
---

# Excel Export

The excel export allows exporting TreeGrid data to Excel document. You need to use the
 [`excelExport`](../api/treegrid/#excelexport) method for exporting. To enable Excel export in the treegrid, set the [`allowExcelExport`](../api/treegrid/#allowexcelexport) as **true**.

To use excel export, You need to inject the **ExcelExport** module in treegrid.

To get start quickly with exporting functionalities, you can check on this video:
`youtube:Rz24Nk4eSEY`

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
            this.treegrid.excelExport();
        }
    }

    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## To customize excel export

The excel export provides an option to customize mapping of the treegrid to excel document.

### Export hidden columns

The excel export provides an option to export hidden columns of treegrid by defining `includeHiddenColumn` as **true**.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ExcelExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
            const excelExportProperties: ExcelExportProperties = {
                includeHiddenColumn: true
            };
            this.treegrid.excelExport(excelExportProperties);
        }
    }

    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration'  visible={false} headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Show or Hide columns on Exported Excel

You can show a hidden column or hide a visible column while printing the treegrid using [`toolbarClick`](../api/treegrid#toolbarclick) and [`excelExportComplete`](../api/grid/excelExportProperties) events.

In the [`toolbarClick`](../api/treegrid#toolbarclick) event, based on **args.item.text** as **Excel Export**. We can show or hide columns by setting [`column.visible`](../api/treegrid/column/#visible) property to *true* or *false* respectively.

In the excelExportComplete event, We have reversed the state back to the previous state.

In the below example, we have *Duration* as a hidden column in the treegrid. While exporting, we have changed *Duration* to visible column and *StartDate* as hidden column.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Column, ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
            const cols: Column[] = this.treegrid.grid.columns as Column[];
            cols[2].visible = false;
            cols[3].visible = true;
            this.treegrid.excelExport();
        }
    }
    public excelExportComplete(): void {
        if (this.treegrid) {
            const cols: Column[] = this.treegrid.grid.columns as Column[];
            cols[3].visible = false;
            cols[2].visible = true;
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration'  visible={false} headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Conditional Cell Formatting

TreeGrid cells in the exported Excel can be customized or formatted using [`excelQueryCellInfo`](../api/treegrid/#excelQueryCellInfo) event. In this event, we can format the treegrid cells of exported PDF document based on the column cell value.

In the below sample, we have set the background color for *Duration* column in the exported excel by **args.cell** and **backgroundColor** property.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { Column, ExcelQueryCellInfoEventArgs, QueryCellInfoEventArgs } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
            this.treegrid.excelExport();
        }
    }
    public excelQueryCellInfo(args: ExcelQueryCellInfoEventArgs): void {
        if (args.column.field === 'duration') {
            if (getValue('data.duration', args) === 0) {
                args.style = {backColor: '#336c12'};
            }
            else if (getValue('data.duration', args) < 3) {
                args.style = {backColor: '#7b2b1d'};
            }
        }
    }

    public queryCellInfo(args: QueryCellInfoEventArgs): void {
        if ((args.column as Column).field === 'duration') {
            if (getValue('data.duration', args) === 0) {
                (args.cell as HTMLElement).style.background= '#336c12';
            } else if (getValue('data.duration', args) < 3) {
                (args.cell as HTMLElement).style.background= '#7b2b1d';
            }
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions} queryCellInfo={this.queryCellInfo} excelQueryCellInfo={this.excelQueryCellInfo}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Theme

The excel export provides an option to include theme for exported excel document.

To apply theme in exported Excel, define the `theme` in `ExcelExportProperties`.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ExcelExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
            const exportProperties: ExcelExportProperties = {
                theme:
                    {
                        caption: { fontName: 'Segoe UI', fontColor: '#666666' },
                        header: { fontName: 'Segoe UI', fontColor: '#666666' },
                        record: { fontName: 'Segoe UI', fontColor: '#666666' }
                    }
                };
            this.treegrid.excelExport(exportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

>By default, material theme is applied to exported excel document.

### To add header and footer

The excel export provides an option to include header and footer content for exported excel document.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ExcelExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
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
            this.treegrid.excelExport(excelExportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### File Name for Exported document

You can assign the file name for the exported document by defining `fileName` property in `ExcelExportProperties`.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Page, Toolbar, ExcelExport, ExcelExportProperties, Inject } from '@syncfusion/ej2-react-treegrid';
import { sampleData } from './datasource';

class App extends React.Component<{}, {}>{

    public toolbarOptions: any = ['ExcelExport'];

    private treegridInstance: TreeGridComponent;

    public toolbarClick(args: ClickEventArgs): void {
        if (args.item.text === 'Excel Export') {
            let excelExportProperties: ExcelExportProperties = {
                fileName:"new.xlsx"
            };
            this.treegridInstance.excelExport(excelExportProperties);
        }
    }

    render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true' pageSettings={{ pageSize: 7 }} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick.bind(this)} ref={ treegrid => this.treegridInstance = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'></ColumnDirective>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'></ColumnDirective>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
ReactDOM.render(<App />, document.getElementById('treegrid'));
```

{% endtab %}

### To persist collapsed state

You can persist the collapsed state in the exported document by defining `isCollapsedStatePersist` property as true in `TreeGridExcelExportProperties` parameter of [`excelExport`](../api/treegrid/#excelexport) method.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Page, Toolbar, ExcelExport, TreeGridExcelExportProperties, Inject } from '@syncfusion/ej2-react-treegrid';
import { sampleData } from './datasource';

class App extends React.Component<{}, {}>{

    public toolbarOptions: any = ['ExcelExport'];

    private treegridInstance: TreeGridComponent;

    public toolbarClick(args: ClickEventArgs): void {
        if (args.item.text === 'Excel Export') {
            let excelExportProperties: TreeGridExcelExportProperties = {
                isCollapsedStatePersist: true
            };
            this.treeGridObj.excelExport(excelExportProperties);
        }
    }

    render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true' pageSettings={{ pageSize: 7 }} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick.bind(this)} ref={ treegrid => this.treegridInstance = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'></ColumnDirective>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'></ColumnDirective>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
ReactDOM.render(<App />, document.getElementById('treegrid'));
```

{% endtab %}

## Custom data source

The excel export provides an option to define datasource dynamically before exporting. To export data dynamically, define the `dataSource` in `ExcelExportProperties`.

{% tab template="treegrid/excel-export", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ExcelExportProperties } from '@syncfusion/ej2-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { ExcelExport, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['ExcelExport'];
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public treegrid: TreeGrid | null;

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Excel Export') {
            const excelExportProperties: ExcelExportProperties = {
                dataSource: sampleData
            };
            this.treegrid.excelExport(excelExportProperties);
        }
    }
    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} allowExcelExport='true' height='220'
        toolbarClick={this.toolbarClick} ref={ treegrid => this.treegrid = treegrid}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, ExcelExport]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}