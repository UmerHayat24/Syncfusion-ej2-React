---
title: "Print"
component: "TreeGrid"
description: "Learn how to print TreeGrid content, set up pages for printing, perform external print, and print visible pages in the Essential JS 2 TreeGrid control."
---

# Print

To print the TreeGrid, use the [`print`](../api/treegrid/#print) method from treegrid instance. The print option can be displayed on the [`toolbar`](../api/treegrid/#toolbar) by adding the **Print** toolbar item.

{% tab template="treegrid/print", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['Print'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='265' toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Page setup

Some of the print options cannot be configured through JavaScript code. So, you have to customize the layout, paper size, and margin options using the browser page setup dialog. Please refer to the following links to know more about the browser page setup:

* [`Chrome`](https://support.google.com/chrome/answer/1069693?hl=en&visit_id=1-636335333734668335-3165046395&rd=1)
* [`Firefox`](https://support.mozilla.org/en-US/kb/how-print-web-pages-firefox)
* [`Safari`](http://www.mintprintables.com/print-tips/adjust-margins-osx/)
* [`IE`](http://www.helpteaching.com/help/print/index.htm)

## Print using an external button

To print the treegrid from an external button, invoke the [`print`](../api/treegrid/#print) method.

{% tab template="treegrid/print", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, Toolbar, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    private treegrid: TreeGrid | null;

    public clickHandler() {
        if (this.treegrid) {
            this.treegrid.print();
        }
    }

    public render() {
        this.clickHandler = this.clickHandler.bind(this);
        return (<div><ButtonComponent onClick= { this.clickHandler}>Print</ButtonComponent>
        <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='265'
         ref={ treegrid => this.treegrid = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar]}/>
        </TreeGridComponent></div>)
    }
}
```

{% endtab %}

## Print the visible page

By default, the treegrid prints all the pages. To print the current page alone, set the [`printMode`](../api/treegrid/#printmode) to **CurrentPage**.

{% tab template="treegrid/print", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, Page, PageSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['Print'];
    public pageSettings: PageSettingsModel = { pageSize: 8 };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='220' toolbar={this.toolbarOptions} allowPaging='true' pageSettings={this.pageSettings}
          printMode='CurrentPage'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar,Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Print large number of columns

By default, the browser uses A4 as page size option to print pages and to adapt the size of the page the browser print preview will auto-hide the overflowed contents. Hence treegrid with large number of columns will cut off to adapt the print page.

To show large number of columns when printing, adjust the scale option from print option panel based on your content size.

![Scale Option Setting](./images/print-preview.png)

## Show or Hide columns while Printing

You can show a hidden column or hide a visible column while printing the treegrid using [`toolbarClick`](../api/treegrid/#toolbarclick) and [`printComplete`](../api/treegrid/#printcomplete) events.

In the [`toolbarClick`](../api/treegrid/#toolbarclick) event, based on **args.item.text** as *Print*. We can show or hide columns by setting [`column.visible`](../api/treegrid/column/#visible) property to *true* or *false* respectively.

In the printComplete event, We have reversed the state back to the previous state.

In the below example, we have **Duration** as a hidden column in the treegrid. While printing, we have changed **Duration** to visible column and **StartDate** as hidden column.

{% tab template="treegrid/print", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Column, Inject, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public toolbarOptions: ToolbarItems[] = ['Print'];

    public toolbarClick(args: any): void {
        if (this.treegrid && args.item.text === 'Print') {
            const cols: Column[] = this.treegrid.grid.columns as Column[];
            for (const col of cols) {
                if (col.field === "duration") {
                    col.visible = true;
                }
                else if (col.field === "startDate") {
                    col.visible = false;
                }
            }
        }
    }

    public printComplete(args: any): void {
        if (this.treegrid) {
            const cols: Column[] = this.treegrid.grid.columns as Column[];
            for (const col of cols) {
                if (col.field === "duration") {
                    col.visible = false;
                }
                else if (col.field === "StartDate") {
                        col.visible = true;
                }
            }
        }
    }

    public render() {
        this.printComplete = this.printComplete.bind(this);
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='265' toolbar={this.toolbarOptions} toolbarClick={this.toolbarClick}
          ref={ treegrid => this.treegrid = treegrid} printComplete={this.printComplete}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' visible={false} />
            </ColumnsDirective>
            <Inject services={[Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Limitations of Printing Large Data

When treegrid contains large number of data, printing all the data at once is not a best option for the browser performance. Because to render all the DOM elements in one page will produce performance issues in the browser. It leads to browser slow down or browser hang.

If printing of all the data is still needed, we suggest to Export the treegrid to **Excel** or **CSV** or **Pdf** and then print it from another non-web based application.