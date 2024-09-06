---
title: "Search"
component: "TreeGrid"
description: "Learn how to search TreeGrid content, change search operators, perform searches using external buttons, and search particular fields."
---

# Search

You can search records in a TreeGrid, by using the [`search`](../api/treegrid/#search) method with search key as a parameter. This also provides an option to integrate search text box in treegrid's toolbar by adding *search* item to the [`toolbar`](../api/treegrid/#toolbar).

To search records, inject the **Filter** module in the grid.

{% tab template="treegrid/searching", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['Search'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270' toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Initial search

To apply search at initial rendering, set the [`fields`](../api/treegrid/searchSettings/#fields), **operator**, [`key`](../api/treegrid/searchSettings/#key), and [`ignoreCase`](../api/treegrid/searchSettings/#ignorecase) in the [`searchSettings`](../api/treegrid/#searchsettings).

{% tab template="treegrid/searching", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, SearchSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['Search'];
    public searchOptions: SearchSettingsModel = {
        fields: ['taskName'],
        ignoreCase: true,
        key: 'plan',
        operator: 'contains'
    };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='270' toolbar={this.toolbarOptions} searchSettings={this.searchOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> By default, treegrid searches all the bound column values. To customize this behavior define the [`searchSettings.fields`](../api/treegrid/searchSettingsModel/#fields) property.

## Search operators

The search operator can be defined in the [`searchSettings.operator`](../api/treegrid/searchSettingsModel/#operator) property to configure specific searching.

The following operators are supported in searching:

Operator |Description
-----|-----
startsWith |Checks whether a value begins with the specified value.
endsWith |Checks whether a value ends with the specified value.
contains |Checks whether a value contains the specified value.
equal |Checks whether a value is equal to the specified value.
notEqual |Checks for values not equal to the specified value.

> By default, the [`searchSettings.operator`](../api/treegrid/searchSettingsModel/#operator) value is *contains*.

## Search by external button

To search treegrid records from an external button, invoke the [`search`](../api/treegrid/#search) method.

{% tab template="treegrid/searching", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public treegrid: TreeGrid | null;
    public inputStyle : object = {width:'200px', display: 'inline-block'};

    public onClick(){
        const searchText: string =
        (document.getElementsByClassName('searchtext')[0] as HTMLInputElement).value;
        if (this.treegrid) {
            this.treegrid.search(searchText);
        }
    }
    public render() {
        this.onClick = this.onClick.bind(this);
        return (<div>
        <div className='e-float-input' style={this.inputStyle}>
            <input type="text" className="searchtext" />
            <span className="e-float-line"/>
            <label className="e-float-text">Search text</label>
        </div>
        <ButtonComponent id='search' onClick= { this.onClick }>Search</ButtonComponent>
        <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='220'
            ref={g => this.treegrid = g}>
            <ColumnsDirective>
                <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
                <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter]}/>
         </TreeGridComponent></div>)
     }
}
```

{% endtab %}}

## Search Specific Columns

By default, treegrid searches all visible columns. You can search specific columns by defining the specific column's field names in the [`searchSettings.fields`](../api/treegrid/searchSettingsModel/#fields) property.

{% tab template="treegrid/searching", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, SearchSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public toolbarOptions: ToolbarItems[] = ['Search'];
    private searchSettings: SearchSettingsModel = {fields: ['taskName', 'duration']};

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         toolbar={this.toolbarOptions} searchSettings={this.searchSettings}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}