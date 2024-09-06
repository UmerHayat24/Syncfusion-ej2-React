---
title: "Scrolling"
component: "TreeGrid"
description: "Learn how to set width and height for TreeGrid content, display a scrollbar and make the TreeGrid responsive with a parent container."
---

# Scrolling

The scrollbar will be displayed in the treegrid when content exceeds the element [`width`](../api/treegrid/#width) or [`height`](../api/treegrid/#height). The vertical and horizontal scrollbars will be displayed based on the following criteria:

* The vertical scrollbar appears when the total height of rows present in the treegrid exceeds its element height.
* The horizontal scrollbar appears when the sum of columns width exceeds the treegrid element width.
* The [`height`](../api/treegrid/#height) and [`width`](../api/treegrid/#width) are used to set the treegrid height and width, respectively.

> The default value for [`height`](../api/treegrid/#height) and [`width`](../api/treegrid/#width) is *auto*.

## Set width and height

To specify the [`width`](../api/treegrid/#width) and [`height`](../api/treegrid/#height) of the scroller in the pixel, set the pixel value to a number.

{% tab template="treegrid/scrolling", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='315' width='400'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='120' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='110' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Responsive with parent container

Specify the [`width`](../api/treegrid/#width) and [`height`](../api/treegrid/#height) as **100%** to make the treegrid element fill its parent container.
Setting the [`height`](../api/treegrid/#height) to **100%** requires the treegrid parent element to have explicit height.

{% tab template="treegrid/responsive-scrolling", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
        height='100%' width='100%'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='120' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='110' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Scroll to selected row

You can scroll the treegrid content to the selected row position by using the [`rowSelected`](../api/treegrid/#rowselected) event.

{% tab template="treegrid/scrolling", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { RowSelectEventArgs } from '@syncfusion/ej2-grids';
import { NumericTextBox, NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public numeric: NumericTextBox | null;

    public onChange(){
        if (this.treegrid && this.numeric) {
            this.treegrid.selectRow(parseInt(this.numeric.getText(), 10));
        }
    }

    public rowSelected(args: RowSelectEventArgs) {
        if (this.treegrid) {
            const rowHeight: number = this.treegrid.getRows()[this.treegrid.getSelectedRowIndexes()[0]].scrollHeight;
            this.treegrid.getContent().children[0].scrollTop = rowHeight * this.treegrid.getSelectedRowIndexes()[0];
        }
    }

    public render() {
        this.onChange = this.onChange.bind(this);
        this.rowSelected = this.rowSelected.bind(this);
        return (<div>
            <NumericTextBoxComponent format={'N'} placeholder={'Enter index to select a row'} width={200}
             showSpinButton={false} min={0} change={this.onChange} ref={(n: any) => this.numeric = n}/>
             <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
              height='270' width='100%' rowSelected={this.rowSelected} ref={g => this.treegrid = g} >
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='160'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent></div>)
    }
}
```

{% endtab %}

## Frozen rows and columns

Frozen rows and columns provides an option to make rows and columns always visible in the top and left side of the treegrid while scrolling.

To use frozen rows and columns support, inject the **Freeze** module in the TreeGrid.

In this demo, the [`frozenColumns`](../api/treegrid/#frozencolumns) is set as **'2'** and the [`frozenRows`](../api/treegrid/#frozenrows)
is set as **'3'**. Hence, the left two columns and top three rows are frozen.

{% tab template="treegrid/frozencolumn", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent, Freeze, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData  } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} childMapping = 'subtasks' treeColumnIndex={1} height='310' frozenRows={3} frozenColumns={2} allowSelection={false} >
            <ColumnsDirective>
                <ColumnDirective field='taskID' headerText='Task ID' width='120' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='taskName' headerText='Task Name' width='230'></ColumnDirective>
                <ColumnDirective field='startDate' headerText='Start Date' width='120' format='yMd' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='endDate' headerText='End Date' width='120' format='yMd' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='duration' headerText='Duration' width='110' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='progress' headerText='Progress' width='110' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='priority' headerText='Priority' width='110'></ColumnDirective>
                <ColumnDirective field='approved' headerText='Approved' textAlign='Center' width='110'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[Freeze]} />
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Freeze particular columns

You can use [`isFrozen`](../api/treegrid/column/#isfrozen) property to freeze selected columns in treegrid.

In this demo, the columns with field name `taskName` and `startDate` is frozen using
the `isFrozen` property.

{% tab template="treegrid/isfrozen", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent, Freeze, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData  } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} childMapping = 'subtasks' height='310' allowSelection={false} >
            <ColumnsDirective>
                <ColumnDirective field='taskID' headerText='Task ID' width='110' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='taskName' headerText='Task Name' width='230' isFrozen='true'></ColumnDirective>
                <ColumnDirective field='startDate' headerText='Start Date' width='120' format='yMd' textAlign='Right' isFrozen='true'></ColumnDirective>
                <ColumnDirective field='endDate' headerText='End Date' width='120' format='yMd' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='duration' headerText='Duration' width='110' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='progress' headerText='Progress' width='110' textAlign='Right'></ColumnDirective>
                <ColumnDirective field='priority' headerText='Priority' width='110'></ColumnDirective>
                <ColumnDirective field='approved' headerText='Approved' textAlign='Center' width='110'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[Freeze]} />
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Limitations

The following features are not supported in frozen rows and columns:

* Row Template
* Detail Template
* Cell Editing