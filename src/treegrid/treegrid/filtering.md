---
title: "Filtering"
component: "TreeGrid"
description: "Learn how to filter rows in the TreeGrid using the filter bar, and menu filtering. Also learn how to use custom filter components in the Essential JS 2 TreeGrid control."
---

# Filtering

Filtering allows you to view specific or related records based on filter criteria. To enable filtering in the TreeGrid, set the [`allowFiltering`](../api/treegrid/#allowfiltering) to true. Filtering options can be configured through [`filterSettings`](../api/treegrid/#filtersettings).

To use filter, inject the **Filter** module in the treegrid.

To get start quickly with filtering functionalities, you can check on this video:
`youtube:_kxndJOgtuw`

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering={true}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * You can apply and clear filtering by using [`filterByColumn`](../api/treegrid/#filterbycolumn) and [`clearFiltering`](../api/treegrid/#clearfiltering) methods.
> * To disable filtering for a particular column, set [`columns.allowFiltering`](../api/treegrid/column/#allowfiltering) to *false*.

## Filter Hierarchy Modes

TreeGrid provides support for a set of filtering modes with [`filterSettings.filterHierarchyMode`](../api/treegrid/filterSettingsModel/#hierarchymode) property.
The below are the type of filter mode available in TreeGrid.

* **Parent** : This is the default filter hierarchy mode in TreeGrid. The filtered records are displayed with its parent records, if the filtered records not have any parent record then the filtered records only displayed.

* **Child** : The filtered records are displayed with its child record, if the filtered records not have any child record then the filtered records only displayed.

* **Both** : The filtered records are displayed with its both parent and child record, if the filtered records not have any parent and child record then the filtered records only displayed.

* **None** : The filtered records are only displayed.

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from "@syncfusion/ej2-react-dropdowns";
import { ColumnDirective, ColumnsDirective, Filter, FilterHierarchyMode } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    private treegrid: TreeGrid | null;
    private data: string[] = ['Parent', 'Child', 'Both', 'None']
    public onChange(sel: ChangeEventArgs): void {
        const mode: FilterHierarchyMode = sel.value.toString() as FilterHierarchyMode;
        if (this.treegrid) {
            this.treegrid.filterSettings.hierarchyMode = mode;
            this.treegrid.clearFiltering();
        }
    }

    public render() {
        this.onChange = this.onChange.bind(this);
        return(<div><DropDownListComponent popupHeight="250px" dataSource={this.data} value="Parent" change={this.onChange} width="150px" />
            <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='225' allowFiltering='true'
            ref={treegrid => this.treegrid = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent></div>)
    }
}
```

{% endtab %}

## Initial filter

To apply the filter at initial rendering, set the filter *predicate* object in
[`filterSettings.columns`](../api/treegrid/filterSettingsModel/#columns).

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public FilterOptions: FilterSettingsModel = {
        columns: [
            { field: 'taskName', matchCase: false, operator: 'startswith', predicate: 'and', value: 'plan' },
            { field: 'duration', matchCase: false, operator: 'equal', predicate: 'and', value: 5 }]
    };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
             height='275' allowFiltering='true' filterSettings={this.FilterOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Filter operators

The filter operator for a column can be defined in the [`operator`](../api/grid/predicate/#operator) property of [`filterSettings.columns`](../api/treegrid/filterSettings/#columns).

The available operators and its supported data types are:

Operator |Description |Supported Types
-----|-----|-----
startswith |Checks whether the value begins with the specified value. |String
endswith |Checks whether the value ends with the specified value. |String
contains |Checks whether the value contains the specified value. |String
equal |Checks whether the value is equal to the specified value. |String &#124; Number &#124; Boolean &#124; Date
notequal |Checks for values not equal to the specified value. |String &#124; Number &#124; Boolean &#124; Date
greaterthan |Checks whether the value is greater than the specified value. |Number &#124; Date
greaterthanorequal|Checks whether a value is greater than or equal to the specified value. |Number &#124; Date
lessthan |Checks whether the value is less than the specified value. |Number &#124; Date
lessthanorequal |Checks whether the value is less than or equal to the specified value. |Number &#124; Date

> By default, the **filterSettings.columns.operator** value is *equal*.

## Filter bar

By setting the [`allowFiltering`](../api/treegrid/#allowfiltering) to true, the filter bar row will render next to the header, which allows you to filter data. You can filter the records with different expressions depending upon the column type.

 **Filter bar expressions:**

 You can enter the following filter expressions (operators) manually in the filter bar.

Expression |Example |Description |Column Type
-----|-----|-----|-----
= |=value |equal |Number
!= |!=value |notequal |Number
> |>value |greaterthan |Number
< |<value |lessthan |Number
>= |>=value |greaterthanorequal |Number
<=|<=value|lessthanorequal |Number
* |*value |startswith |String
% |%value |endswith |String
N/A |N/A | *Equal* operator will always be used for date filter. |Date
N/A |N/A |*Equal* operator will always be used for Boolean filter. |Boolean

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> By default, the [`filterSettings.columns.operator`](../api/treegrid/filterSettingsModel/#operators) value is *equal*.

## Filterbar template with custom component

You can customize default filter bar component of a column by custom component using **filter template**.

The following example demonstrates the way to use filter template for a column when using filter bar. In the following example, the DropdownList component is used to filter **duration** column using filter template.

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ColumnDirective, ColumnsDirective, Filter } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;

    public onChange(args: any): any{
        if (this.treegrid) {
          if (args.value === 'All') {
            this.treegrid.clearFiltering();
          } else {
            this.treegrid.filterByColumn('duration', 'equal', parseInt(args.value, 0));
          }
        }
      }
      public templateOptions(props:any): any {
        this.onChange = this.onChange.bind(this);
        const dataSource: string[] = ['All', '1', '3', '4', '5', '6', '8', '9'];
        return (<DropDownListComponent id={props.column.field} popupHeight='250px' dataSource={dataSource} change={this.onChange} /> );
      }

    public render() {
        this.templateOptions = this.templateOptions.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true' ref={treegrid => this.treegrid = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' filterTemplate={this.templateOptions} />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Change default filter bar operator

You can change the default filter operator by extending [`filterModule.filterOperators`](../api/treegrid/filterSettings/#operators) property in [`dataBound`](../api/treegrid/#databound) event.

In the following sample, we have changed the default operator for string typed columns as `contains` from `startsWith`.

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, Filter } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid'
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public dataBound(args){
            Object.assign(this.treegrid.grid.filterModule.filterOperators,{ startsWith: 'contains' });
    }

    public render() {
           this.dataBound=this.dataBound.bind(this);
           return <TreeGridComponent dataSource={sampleData} dataBound={this.dataBound} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true' ref={treegrid => this.treegrid = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' filterTemplate={this.templateOptions} />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}

```

{% endtab %}

## Filter menu

You can enable filter menu by setting the [`filterSettings.type`](../api/treegrid/filterSettingsModel/#type) as *Menu*. The filter menu UI will be rendered based on its column type, which allows you to filter data.
You can filter the records with different operators.

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter } from '@syncfusion/ej2-react-treegrid';
import { FilterSettingsModel, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public FilterOptions: FilterSettingsModel = {
        type: 'Menu'
    };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true' filterSettings={this.FilterOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * [`allowFiltering`](../api/treegrid/#allowfiltering) must be set as true to enable filter menu.
> * Setting [`columns.allowFiltering`](../api/treegrid/column/#allowfiltering) as false will prevent filter menu rendering for a particular column.

### Custom component in filter menu

You can customize default filter menu component of a column by custom component using **filterTemplate**.

The following example demonstrates the way to use filter template for a column when using filter menu. In the following example, the DropdownList component is used to filter **duration** column using **filterTemplate**.

<!--{% tab template="treegrid/filtering", sourceFiles="app/App.tsx" %}-->

```typescript
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public FilterOptions: FilterSettingsModel = {
        type: 'Menu'
    };
    public templateOptions(props:any): any {
        const dataSource: number[] = [1,3,4,5,6,8,9];
        return (<DropDownListComponent id={props.column.field} popupHeight='250px' dataSource={dataSource} /> );
    }

    public render() {
        this.templateOptions = this.templateOptions.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} filterSettings={this.FilterOptions} childMapping='subtasks' height='275' allowFiltering='true' ref={treegrid => this.treegrid = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' filterTemplate={this.templateOptions} />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

<!--{% endtab %}-->

### Enable different filter for a column

You can use both *Menu* and *Excel* filter in a same TreeGrid. To do so, set the
[`column.filter.type`](../api/treegrid/column/#filter) as *Menu* or *Excel*.

In the following sample menu filter is enabled by default and excel filter is enabled for the Task Name column using the
[`column.filter.type`](../api/treegrid/column/#filter).

{% tab template="treegrid/filtering", sourceFiles="app/filter.tsx", compileJsx=true %}

```typescript
import { IFilter } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public FilterOptions: FilterSettingsModel = {
        type: 'Menu'
    };
    public Filter : IFilter = {
        type: 'Excel'
    }
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true' filterSettings={this.FilterOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' filter={this.Filter} width='180' />
              <ColumnDirective field='duration' headerText='Duration' width='90'/>
              <ColumnDirective field='progress' headerText='Progress' width='90'/>
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Excel Filter

You can enable Excel like filter by defining [`filterSettings.type`](../api/treegrid/filterSettingsModel/#type) as *Excel*. The excel menu contains an option such as Sorting, Clear filter, Sub menu for advanced filtering..

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public FilterOptions: FilterSettingsModel = {
        type: 'Excel'
    };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true' filterSettings={this.FilterOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' />
              <ColumnDirective field='duration' headerText='Duration' width='90'/>
              <ColumnDirective field='progress' headerText='Progress' width='90'/>
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Change default filter operator

You can change the default excel-filter operator by changing the column operator as `contains` from `startsWith` in the [`actionBegin`](../api/treegrid/#actionBegin) event

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public FilterOptions: FilterSettingsModel = {
        type: 'Excel'
    };
    public actionBegin(args){
      if(args.requestType === 'filtersearchbegin' && args.column.type === "string")
      {
        args.operator = 'contains';
      }
    }
    public render() {
        this.actionBegin=this.actionBegin.bind(this)
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' allowFiltering='true' filterSettings={this.FilterOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' />
              <ColumnDirective field='duration' headerText='Duration' width='90'/>
              <ColumnDirective field='progress' headerText='Progress' width='90'/>
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Diacritics

By default, treegrid ignores diacritic characters while filtering. To include diacritic characters, set the [`filterSettings.ignoreAccent`](../api/treegrid/filterSettingsModel/#ignoreaccent) as **true**.

In the following sample, type **aero** in *Name* column to filter diacritic characters.

{% tab template="treegrid/filtering", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Filter, FilterSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { diacritics } from './datasource';

export default class App extends React.Component<{}, {}>{
    public FilterOptions: FilterSettingsModel = {
        ignoreAccent: true
    };

    public render() {
        return <TreeGridComponent dataSource={diacritics} treeColumnIndex={0} childMapping='Children'
            height='275' allowFiltering='true' filterSettings={this.FilterOptions}>
            <ColumnsDirective>
              <ColumnDirective field='EmpID' headerText='Employee ID' width='95'/>
              <ColumnDirective field='Name' headerText='Name' width='180'/>
              <ColumnDirective field='DOB' headerText='DOB' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='Country' headerText='Country' width='100' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}
