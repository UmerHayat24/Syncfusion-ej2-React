---
title: "Paging"
component: "TreeGrid"
description: "Learn how to add and customize the pager in the Essential JS 2 TreeGrid control."
---

# Paging

Paging provides an option to display TreeGrid data in page segments. To enable paging, set the [`allowPaging`](../api/treegrid/#allowpaging) to **true**. When paging is enabled, pager component renders at the bottom of the treegrid.
Paging options can be configured through the [`pageSettings`](../api/treegrid/#pagesettings).

To use Paging, inject **Page** module in TreeGrid.

{% tab template="treegrid/paging", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> You can achieve better performance by using treegrid paging to fetch only a pre-defined number of records from the data source.

## Page Size Mode

Two behaviors are available in TreeGrid paging to display certain number of records in a current page. Following are the two types of [`pageSizeMode`](../api/treegrid/pageSettingsModel/#pagesizemode).

* **All** : This is the default mode. The number of records in a page is based on [`pageSize`](../api/treegrid/pageSettingsModel/#pagesize) property.
* **Root** : The number of root nodes or the 0th level records to be displayed per page is based on [`pageSize`](../api/treegrid/pageSettingsModel/#pagesize) property.

With [`pageSizeMode`](../api/treegrid/pageSettingsModel/#pagesizemode) property as **Root** only the root level or the 0th level records are considered in records count.

{% tab template="treegrid/paging", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 2, pageSizeMode: 'Root' };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
         pageSettings={this.pageSettings} height='265'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='160'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Template

You can use custom elements inside the pager instead of default elements.
The custom elements can be defined by using the [`template`](../api/treegrid/pageSettingsModel/#template) property.
Inside this template, you can access the [`currentPage`](../api/treegrid/pageSettingsModel/#currentpage), [`pageSize`](../api/treegrid/pageSettingsModel/#pagesize), [`pageCount`](../api/treegrid/pageSettingsModel/#pagecount), **totalPage** and **totalRecordCount** values.

{% tab template="treegrid/paging", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs } from '@syncfusion/ej2-inputs';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { ColumnDirective, ColumnsDirective, Inject, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = {
        pageSize: 6,
        template: this.pageTemplate.bind(this)
    };
    public treegrid: TreeGrid | null;

    public pageTemplate(props: any): any {
        return (<div className="e-pagertemplate">
           <div className="col-lg-12 control-section">
              <div className="content-wrapper">
                <NumericTextBoxComponent max={3} min={1} step={1} value={props.currentPage} width={75} format='###.##' change={this.onChange}/>
               </div>
           </div>

           <div id="totalPages" className="e-pagertemplatemessage">
              <span className="e-pagenomsg">{props.currentPage} of {props.totalPages} pages ({props.totalRecordsCount} items)</span>
           </div>
        </div>);
    }

    public onChange(args: ChangeEventArgs) {
        const value: number = args.value as number;
        if (this.treegrid) {
            this.treegrid.goToPage(value);
        }
    }


    public render() {
        this.onChange = this.onChange.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='160'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Pager with Page Size Dropdown

The pager Dropdown allows you to change the number of records in the TreeGrid dynamically. It can be enabled by defining the [`pageSettings.pageSizes`](../api/treegrid/pageSettingsModel/#pagesizes) property as **true**.

```typescript
    public pageSettings: PageSettingsModel = { pageSize: 7, pageSizes: true };
```

![Page size dropdown](images/pagesizes.png)

## How to render Pager at the Top of the TreeGrid

By default, Pager will be rendered at the bottom of the TreeGrid. You can also render the Pager at the top of the TreeGrid by using the [`dataBound`](../api/treegrid/#databound) event.

{% tab template="treegrid/paging", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public pageSettings: PageSettingsModel = { pageSize: 7, pageSizes: true };
    public initialGridLoad: boolean = true;

    public dataBound() {
        if (this.initialGridLoad) {
            this.initialGridLoad = false;
            const pager = document.getElementsByClassName('e-gridpager');
            let topElement;
            if (this.treegrid && this.treegrid.toolbar) {
                topElement = document.getElementsByClassName('e-toolbar');
            } else {
                topElement = document.getElementsByClassName('e-gridheader');
            }
            topElement[0].before(pager[0]);
        }
    }

    public render() {
        this.dataBound = this.dataBound.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
             pageSettings={this.pageSettings} dataBound={this.dataBound} ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> During the paging action, the pager component triggers the below three events.
> * The [`created`](../api/pager/#created) event triggers when Pager is created.
> * The [`click`](../api/pager/#click) event triggers when the numeric items in the pager is clicked.
> * The [`dropDownChanged`](../api/pager/#dropdownchanged) event triggers when pageSize DropDownList value is selected.
