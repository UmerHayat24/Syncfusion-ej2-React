---
title: "Getting Started"
component: "TreeGrid"
description: "Learn how to create a TreeGrid and to enable the features like paging, filtering, sorting and in React."
---

# Getting started

This section explains the steps required to create a simple Essential JS 2 TreeGrid and demonstrates the basic usage of the TreeGrid control in a React application.

To get start quickly with React Tree Grid, you can check on this video:

`youtube:dQcIAoSgARc`

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install **create-react-app** run the following command.

```sh
npm install -g create-react-app
```

* To setup basic **React** sample use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

## Adding Syncfusion TreeGrid packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
To install TreeGrid component, use the following command

```sh
npm install @syncfusion/ej2-react-treegrid --save
```

## Adding CSS reference

 Add components style as given below in **src/App.css**.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import "../node_modules/@syncfusion/ej2-grids/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-treegrid/styles/material.css";
```

> To refer **App.css** in the application then import it in the **src/App.tsx** file.

## Adding TreeGrid component

Now, you can start adding TreeGrid component in the application. For getting started, add the TreeGrid component in **src/App.tsx** file
using following code.

Place the following treegrid code in the **src/App.tsx**.

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping= 'subtasks'>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='150'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='170'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='130' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='price' headerText='Price' width='100' textAlign='Right' type='number' format='C0' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

## Module Injection

TreeGrid component features are segregated into individual feature-wise modules.
In order to use a particular feature, you need to inject its feature service in the `App`.
In the current application, we are going to use paging, sorting, filtering and exporting feature of TreeGrid.
Please find relevant feature service name and description as follows.

* **Page** - Inject this service to use paging feature.
* **Sort** - Inject this service to use sorting feature.
* **Filter** - Inject this service to use filtering feature.
* **ExcelExport** - Inject this service to use Excel Export feature.
* **PdfExport** - Inject this service to use PDF Export feature.

These modules should be injected into the treegrid using the **Inject** directive.

> Additional feature modules are available [`here`](./module).

## Enable Paging

The paging feature enables users to view the TreeGrid record in a paged view.
It can be enabled by setting [`allowPaging`](../api/treegrid/#allowpaging) property to true.
Inject the **Page** module in **Inject.services** as follows.
If the **Page** service is not injected, the pager will not be rendered in the treegrid.
Pager can be customized using [`pageSettings`](../api/treegrid/pageSettings) property.

We also have Root level paging mode in which paging is based on the root level rows only i.e., it ignores the child rows count and it can be enabled by using the [`pageSettings.pageSizeMode`](../api/treegrid/pageSettings/#pagesizemode) property.

{% tab template="treegrid/getting-started", sourceFiles="app/App.tsx,app/data.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, Inject, Page, Sort } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './data';

export default class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = { pageSize: 2 };
    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping= 'subtasks'
            allowPaging='true'>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='150'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='170'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='130' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='price' headerText='Price' width='100' textAlign='Right' type='number' format='C0' />
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Enable Sorting

The sorting feature enables you to order the records.
It can be enabled by setting the [`allowSorting`](../api/treegrid/#allowsorting) property as *true*.
Inject the **Sort** module in the **Inject.services** as follows.
If the **Sort** module is not injected, you cannot sort when a header is clicked.
Sorting feature can be customized using [`sortSettings`](../api/treegrid/#sortsettings) property.

{% tab template="treegrid/getting-started", sourceFiles="app/App.tsx,app/data.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, Inject, Page, Sort, SortSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './data';

export default class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = { pageSize: 7 };
    public sortingOptions: SortSettingsModel = {
        columns: [
            { field: 'Category', direction: 'Ascending' },
            { field: 'orderName', direction: 'Ascending' }
        ]
    };

    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping= 'subtasks'
            allowPaging='true' allowSorting='true' sortSettings={this.sortingOptions}>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='150'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='170'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='130' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='price' headerText='Price' width='100' textAlign='Right' type='number' format='C0' />
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Enable Filtering

The filtering feature enables you to view reduced amount of records based on filter criteria. It can be enabled by setting the [`allowFiltering`](../api/treegrid/#allowfiltering) property as true.
Inject the **Filter** module in the **Inject.services** as follows.
If **Filter** module is not injected, filter bar will not be rendered in TreeGrid.
Filtering feature can be customized using [`filterSettings`](../api/treegrid/filterSettings) property.

By default, filtered records are shown along with its parent records. This behavior can be changed by using [`filterSettings-hierarchyMode`](../api/treegrid/filterSettings/#hierarchyMode) property.

{% tab template="treegrid/getting-started", sourceFiles="app/App.tsx,app/data.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, FilterSettingsModel, Inject, Page, Sort, SortSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './data';

export default class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = { pageSize: 7 };
    public sortingOptions: SortSettingsModel = {
        columns: [
            { field: 'Category', direction: 'Ascending' },
            { field: 'orderName', direction: 'Ascending' }
        ]
    };
    public filterSettings: FilterSettingsModel = { columns: [
        {field: 'price', operator: 'lessthan', value: 40 }
    ] };
    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping= 'subtasks'
            allowPaging='true' allowSorting='true' allowFiltering={true} filterSettings = {this.filterSettings} sortSettings={this.sortingOptions}>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='150'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='170'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='130' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='price' headerText='Price' width='100' textAlign='Right' type='number' format='C0' />
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Run the application

The [`create-react-app`](https://github.com/facebookincubator/create-react-app) will pre-configure the project to compile and
run the application in browser. Use the following command to run the application.

```sh

npm start

```

Output will be appears as follows.

{% tab template="treegrid/getting-started", sourceFiles="app/App.tsx,app/data.tsx", isDefaultActive = true, compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, FilterSettingsModel, Inject, Page, Sort, SortSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sortData } from './data';

export default class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = { pageSize: 7 };
    public sortingOptions: SortSettingsModel = {
        columns: [
            { field: 'Category', direction: 'Ascending' },
            { field: 'orderName', direction: 'Ascending' }
        ]
    };
    public filterSettings: FilterSettingsModel = { columns: [
        {field: 'price', operator: 'lessthan', value: 40 }
    ] };
    public render() {
        return <TreeGridComponent dataSource={sortData} treeColumnIndex={1} childMapping= 'subtasks'
            allowPaging='true' allowSorting='true' allowFiltering={true} filterSettings = {this.filterSettings} sortSettings={this.sortingOptions}>
            <ColumnsDirective>
              <ColumnDirective field='Category' headerText='Category' width='150'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='170'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='130' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='price' headerText='Price' width='100' textAlign='Right' type='number' format='C0' />
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}