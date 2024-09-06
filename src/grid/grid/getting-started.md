---
title: "Getting Started"
component: "Grid"
description: "Learn how to create an Essential JS 2 DataGrid control and enable features like paging, filtering, sorting, and grouping."
---

# Getting started

This section explains you the steps required to create a simple Grid and demonstrate the basic usage of the Grid component in React environment.

To get start quickly with React Grid, you can check on this video:

`youtube:QNwcXokKc70`

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install **create-react-app** run the following command.

```sh
npm install -g create-react-app
```

To setup basic **React** sample, use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

## Adding Syncfusion Grid packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
To install Grid component, use the following command

```sh
npm install @syncfusion/ej2-react-grids --save
```

> The --save will instruct NPM to include the Grid package inside of the **dependencies** section of the package.json.

## Adding CSS reference

The following CSS files are available in **../node_modules/@syncfusion** package folder. This can be added as reference in **src/App.css**.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import "../node_modules/@syncfusion/ej2-react-grids/styles/material.css";
```

> To refer **App.css** in the application then import it in the **src/App.tsx** file.

## Adding Grid component

Now, you can start adding React Grid component in the application. For getting started, add the Grid component in **src/App.tsx** file
using following code.

Place the following grid code in the **src/App.tsx**.

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <GridComponent dataSource={data}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' width='100'/>
                <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' width='100'/>
            </ColumnsDirective>
        </GridComponent>
    }
};
```

## Module Injection

React Grid component features are segregated into individual feature-wise modules.
In order to use a particular feature, you need to inject its feature service in the **App**.
In the current application, we are going to use paging, sorting, filtering and grouping feature of Grid.
Please find relevant feature service name and description as follows.

* **Page** - Inject this service to use paging feature.
* **Sort** - Inject this service to use sorting feature.
* **Filter** - Inject this service to use filtering feature.
* **Group** - Inject this service to use grouping feature.

These modules should be injected into the grid using the **Inject** directive.

> Additional feature modules are available [`here`](./module).

## Enable Paging

The paging feature enables users to view the Grid record in a paged view.
It can be enabled by setting [`allowPaging`](../api/grid/#allowpaging) property to true.
Inject the **Page** module in **Inject.services** as follows.
If the **Page** service is not injected, the pager will not be rendered in the grid.
Pager can be customized using [`pageSettings`](../api/grid/#pagesettings) property.

{% tab template="grid/getting-started", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, GridComponent, Group, Inject, Page, PageSettingsModel, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 6 }
    public render() {
        return <GridComponent dataSource={data} allowPaging={true} pageSettings={ this.pageSettings }>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' width='100'/>
                <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' width='100'/>
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter, Group]} />
        </GridComponent>
    }
};
```

{% endtab %}

## Enable Sorting

The sorting feature enables you to order the records.
It can be enabled by setting the [`allowSorting`](../api/grid/#allowsorting) property as true.
Inject the **Sort** module in the **Inject.services** as follows.
If the **Sort** module is not injected, you cannot sort when a header is clicked.
Sorting feature can be customized using [`sortSettings`](../api/grid/#sortsettings) property.

{% tab template="grid/getting-started", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, GridComponent, Group } from '@syncfusion/ej2-react-grids';
import { Inject, Page, PageSettingsModel, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 6 }
    public sortSettings: SortSettingsModel = { columns: [
                            {field: 'EmployeeID', direction: 'Ascending' }
                        ] };
    public render() {
        return <GridComponent dataSource={data} allowPaging={true} pageSettings={ this.pageSettings }
            allowSorting={true} sortSettings={ this.sortSettings }>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' width='100'/>
                <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' width='100'/>
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter, Group]} />
        </GridComponent>
    }
};
```

{% endtab %}

## Enable Filtering

It can be enabled by setting the [`allowFiltering`](../api/grid/#allowfiltering) property as true.
Inject the [`Filter`](../api/grid/#filtermodule) module in the **Inject.services** as follows.
If [`Filter`](../api/grid/#filtermodule) module is not injected, filter bar will not be rendered in Grid.
Filtering feature can be customized using [`filterSettings`](../api/grid/#filtersettings) property.

{% tab template="grid/getting-started", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel, GridComponent } from '@syncfusion/ej2-react-grids';
import {  Group, Inject, Page, PageSettingsModel, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 6 }
    public sortSettings: SortSettingsModel = { columns: [
                            {field: 'EmployeeID', direction: 'Ascending' }
                        ] };
    public filterSettings: FilterSettingsModel = { columns: [
                            {field: 'EmployeeID', operator: 'greaterthan', value: 2 }
                        ] };
    public render() {
        return <GridComponent dataSource={data} allowPaging={true} pageSettings={ this.pageSettings }
                filterSettings = {this.filterSettings}
                allowSorting={true} sortSettings={ this.sortSettings } allowFiltering={true}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' width='100'/>
                <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' width='100'/>
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter, Group]} />
        </GridComponent>
    }
};
```

{% endtab %}

## Enable Grouping

The grouping feature enables you to view the grid record in a grouped view.
It can be enabled by setting [`allowGrouping`](../api/grid/#allowgrouping) property to true.
The [`Group`](../api/grid/#groupmodule) module has to be injected as follows.
If [`Group`](../api/grid/#groupmodule) module is not injected, the group drop area will not be rendered in Grid.
Grouping feature can be customized using [`groupSettings`](../api/grid/#groupsettings) property.

{% tab template="grid/getting-started", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel, GridComponent, Group, GroupSettingsModel } from '@syncfusion/ej2-react-grids';
import {Inject, Page, PageSettingsModel, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 6 }
    public sortSettings: SortSettingsModel = { columns: [
                            {field: 'EmployeeID', direction: 'Ascending' }
                        ] };
    public filterSettings: FilterSettingsModel = { columns: [
                            {field: 'EmployeeID', operator: 'greaterthan', value: 2 }
                        ] };
    public groupSettings: GroupSettingsModel = { columns: ['EmployeeID'] };
    public render() {
        return <GridComponent dataSource={data} allowPaging={true} pageSettings={ this.pageSettings }
                filterSettings = {this.filterSettings} allowGrouping={true} groupSettings={ this.groupSettings }
                allowSorting={true} sortSettings={ this.sortSettings } allowFiltering={true} height={180}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' width='100'/>
                <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' width='100'/>
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter, Group]} />
        </GridComponent>
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

{% tab template="grid/getting-started", sourceFiles="app/App.tsx,app/datasource.tsx" , isDefaultActive = true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel, GridComponent, Group, GroupSettingsModel } from '@syncfusion/ej2-react-grids';
import {Inject, Page, PageSettingsModel, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: PageSettingsModel = { pageSize: 6 }
    public sortSettings: SortSettingsModel = { columns: [
                            {field: 'EmployeeID', direction: 'Ascending' }
                        ] };
    public filterSettings: FilterSettingsModel = { columns: [
                            {field: 'EmployeeID', operator: 'greaterthan', value: 2 }
                        ] };
    public groupSettings: GroupSettingsModel = { columns: ['EmployeeID'] };
    public render() {
        return <GridComponent dataSource={data} allowPaging={true} pageSettings={ this.pageSettings }
                filterSettings = {this.filterSettings} allowGrouping={true} groupSettings={ this.groupSettings }
                allowSorting={true} sortSettings={ this.sortSettings } allowFiltering={true} height={180}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' width='100'/>
                <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' width='100'/>
            </ColumnsDirective>
            <Inject services={[Page, Sort, Filter, Group]} />
        </GridComponent>
    }
};

```

{% endtab %}

> You can refer to our [React Grid](https://www.syncfusion.com/react-ui-components/react-data-grid) feature tour page for its groundbreaking feature representations. You can also explore our [React Grid Component example](https://ej2.syncfusion.com/react/demos/#/material/grid/overview) that shows how to render the Grid in React.

## See also

* [Top 5 Features of React Data Grid](https://www.syncfusion.com/blogs/post/top-5-features-react-data-grid.aspx)
* [How to render React Grid with bootstrap theme](https://www.syncfusion.com/kb/11328/how-to-render-react-grid-with-bootstrap-theme)