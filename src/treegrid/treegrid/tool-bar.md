---
title: "ToolBar"
component: "TreeGrid"
description: "Learn how to use the toolbar and add custom toolbar items in the Essential JS 2 TreeGrid control."
---

# ToolBar

The TreeGrid provides ToolBar support to handle treegrid actions. The [`toolbar`](../api/treegrid/#toolbar)
property accepts either the collection of built-in toolbar items and [`ItemModel`](../api/toolbar/itemModel/)objects for custom toolbar items or HTML element ID for toolbar template.

To use ToolBar, inject **Toolbar** module in the treegrid.

## Built-in toolbar items

Built-in toolbar items execute standard actions of the treegrid, and it can be added by defining the [`toolbar`](../api/treegrid/#toolbar)
as a collection of built-in items. It renders the button with icon and text.

The following table shows built-in toolbar items and its actions.

| Built-in Toolbar Items | Actions |
|------------------------|---------|
| ExpandAll | Expands all the rows.|
| CollapseAll | Collapses all the rows.|
| Add | Adds a new record.|
| Edit | Edits the selected record.|
| Update | Updates the edited record.|
| Delete | Deletes the selected record.|
| Cancel | Cancels the edit state.|
| Search | Searches the records by the given key.|
| Print | Prints the treegrid.|
| ExcelExport | Exports the treegrid to Excel.|
| PdfExport | Exports the treegrid to PDF.|
| WordExport | Exports the treegrid to Word.|

{% tab template="treegrid/toolbar", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['Print', 'Search'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='265' toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar,Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * The [`toolbar`](../api/treegrid/#toolbar) has options to define both built-in and custom toolbar items.

## Custom toolbar items

Custom toolbar items can be added by defining the [`toolbar`](../api/treegrid/#toolbar) as a collection of
[`ItemModels`](../api/toolbar/itemModel/).
Actions for this customized toolbar items are defined in the [`toolbarClick`](../api/treegrid/#toolbarclick) event.

By default, Custom toolbar items are in position **Left**. You can change the position by using the [`align`](../api/toolbar/itemModel/#align) property. In the below sample, we have applied position **Right** for the **Quick Filter** toolbar item.

{% tab template="treegrid/toolbar", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, Inject, Toolbar, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;

    public toolbarOptions: object[] = [
        { text: 'Quick Filter', tooltipText: 'Quick Filter', id: 'toolbarfilter', align:'Right' }
    ];

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Quick Filter') {
            this.treegrid.filterByColumn("taskName","startswith","Testing");
        }
    }

    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowFiltering={true} height='220' toolbar={this.toolbarOptions} toolbarClick={this.toolbarClick}
          ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='160'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar,Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * The [`toolbar`](../api/treegrid/#toolbar) has options to define both built-in and custom toolbar items.
> * If a toolbar item does not match the built-in items, it will be treated as a custom toolbar item.

## Built-in and custom items in toolbar

TreeGrid have an option to use both built-in and custom toolbar items at same time.

In the below example, **ExpandAll**, **CollapseAll** are built-in toolbar items and *Click* is custom toolbar item.

{% tab template="treegrid/toolbar", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, Toolbar, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;

    public toolbarOptions: any[] = [
        'ExpandAll', 'CollapseAll',
        { text: 'Click', tooltipText: 'Click', id: 'Click', prefixIcon:'e-time' }];

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid && args.item.text === 'Click') {
            alert("Custom toolbar click...");
        }
    }

    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         ref={g => this.treegrid = g} toolbar={this.toolbarOptions} toolbarClick={this.toolbarClick}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='160'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Enable/disable toolbar items

You can enable/disable toolbar items by using the `enableItems` method.

{% tab template="treegrid/toolbar", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, Inject, Toolbar, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;

    public toolbarOptions: string[] = ['QuickFilter', 'ClearFilter'];

    public enable() {
        if (this.treegrid) {
            // Enable toolbar items.
            this.treegrid.toolbarModule
                .enableItems([this.treegrid.element.id + '_gridcontrol_QuickFilter', this.treegrid.element.id + '_gridcontrol_ClearFilter'], true);
        }
    }

    public disable() {
        if (this.treegrid) {
            // Disable toolbar items.
            this.treegrid.toolbarModule
                .enableItems([this.treegrid.element.id + '_gridcontrol_QuickFilter', this.treegrid.element.id + '_gridcontrol_ClearFilter'], false);
        }
    }

    public toolbarClick(args: ClickEventArgs): void {
        if (this.treegrid) {
            if (args.item.text === 'QuickFilter') {
                this.treegrid.filterByColumn('taskName', 'startswith', 'Testing');
            }
            if (args.item.text === 'ClearFilter') {
                this.treegrid.clearFiltering();
            }
        }
    }

    public render() {
        this.toolbarClick = this.toolbarClick.bind(this);
        this.enable = this.enable.bind(this);
        this.disable = this.disable.bind(this);
        return (<div><ButtonComponent className='e-flat' onClick= { this.enable }>Enable</ButtonComponent>
        <ButtonComponent className='e-flat' onClick= { this.disable }>Disable</ButtonComponent>
        <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='200'
         ref={g => this.treegrid = g} toolbar={this.toolbarOptions} toolbarClick={this.toolbarClick} allowFiltering='true'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Toolbar,Filter]}/>
        </TreeGridComponent></div>)
    }

}
```

{% endtab %}
