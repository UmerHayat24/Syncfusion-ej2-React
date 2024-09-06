---
title: "Selection"
component: "TreeGrid"
description: "Learn how to select rows and cells, use range selection, and use check box selection in the Essential JS 2 TreeGrid control."
---

# Selection

Selection provides an option to highlight a row or cell.
Selection can be done through simple Mouse down or Arrow keys.
To disable selection in the TreeGrid, set the [`allowSelection`](../api/treegrid/#allowselection) to **false**.

To get start quickly with Selection, you can check on this video:

`youtube:2pAN-4v7E4E`

The treegrid supports two types of selection that can be set by using the
[`selectionSettings.type`](../api/treegrid/selectionSettings/#type).They are:

* **Single** - It is set by default. Allows you to select only a single row or cell.
* **Multiple** - Allows you to select multiple rows or cells.
To perform the multi-selection, press and hold CTRL key and click the desired rows or cells.
To select range of rows or cells, press and hold the SHIFT key and click the rows or cells.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = { type: 'Multiple' };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
         selectionSettings={this.settings}>
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

## Selection Mode

TreeGrid supports three types of selection mode which can be set by using
[`selectionSettings.mode`](../api/treegrid/selectionSettings/#mode). They are:

* **Row** - It is set by default. Allows you to select rows only.
* **Cell** - Allows you to select cells only.
* **Both** - Allows you to select rows and cells at the same time.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = { mode: 'Both' };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
         selectionSettings={this.settings}>
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

## Cell Selection

Cell Selection can be done through simple Mouse down or Arrow keys(up, down, left and right).

TreeGrid supports two types of cell selection mode which can be set by using
[`selectionSettings.cellSelectionMode`](../api/treegrid/selectionSettings/#cellselectionmode). They are:

* **Flow** - It is set by default.
Select range of cells between the start index and end index which includes in between cells of rows.
* **Box** - Select range of cells within the start and end column indexes which includes
in between cells of rows within the range.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = {
        cellSelectionMode: 'Box',
        mode: 'Cell',
        type: 'Multiple'
    };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
         selectionSettings={this.settings}>
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

## Checkbox selection

Checkbox Selection provides an option to select multiple TreeGrid records with help of checkbox in each row.

To render checkbox in each treegrid row, you need to use checkbox column with type as **CheckBox** using column [`type`](../api/treegrid/column/#type) property.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={2} childMapping='subtasks' allowPaging='true'>
            <ColumnsDirective>
              <ColumnDirective type='checkbox' width='50'/>
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

> By default selection is allowed by clicking a treegrid row or checkbox in that row. To allow Selection only through checkbox, you can set
[`selectionSettings.checkboxOnly`](../api/treegrid/selectionSettings/#checkboxonly) property to **true**.
> Selection can be persisted on all the operations
using [`selectionSettings.persistSelection`](../api/treegrid/selectionSettings/#persistselection) property.
For persisting selection on the TreeGrid, any one of the column should be defined as a primary key using [`columns.isPrimaryKey`](../api/treegrid/column/#isprimarykey) property.

### Checkbox selection Mode

In checkbox selection, selection can also be done by clicking on rows. This selection provides two types of Checkbox Selection mode which can be set by using the following API,
[`selectionSettings.checkboxMode`](../api/treegrid/selectionSettings/#checkboxmode). The modes are;

* **Default**: This is the default value of the checkboxMode. In this mode, user can select multiple rows by clicking rows one by one.
* **ResetOnRowClick**: In ResetOnRowClick mode, when user clicks on a row it will reset previously selected row. Also you can perform multiple-selection in this mode by press
and hold CTRL key and click the desired rows. To select range of rows, press and hold the SHIFT key and click the rows.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = { checkboxMode: 'ResetOnRowClick'};
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={2} childMapping='subtasks' allowPaging='true'
        selectionSettings={this.settings}>
            <ColumnsDirective>
              <ColumnDirective type='checkbox' width='50'/>
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

## Toggle selection

The Toggle selection allows to perform selection and unselection of the particular row or cell. To enable toggle selection, set [`enableToggle`](../api/treegrid/selectionSettings/#enable toggle) property of the selectionSettings as true. If you click on the selected row or cell then it will be unselected and vice versa.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = { enableToggle: true};
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
        selectionSettings={this.settings}>
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

>If multi selection is enabled, then first click on any selected row (without pressing Ctrl key), it will clear the multi selection and in second click on the same row, it will be unselected.

## Select row at Initial rendering

To select a row at initial rendering, set the [`selectedRowIndex`](../api/treegrid/#selectedrowindex) value.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true'
        selectedRowIndex={1}>
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

## Get selected row indexes

You can get the selected row indexes by using the [`getSelectedRowIndexes`](../api/treegrid/#getselectedrowindexes) method.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public settings: SelectionSettingsModel = { type: 'Multiple' };

    public rowSelected() {
        if (this.treegrid) {
            /** Get the selected row indexes */
            const selectedrowindex: number[] = this.treegrid.getSelectedRowIndexes();
            /** Get the selected records. */
            const selectedrecords: object[] = this.treegrid.getSelectedRecords();
            alert(selectedrowindex + " : " + JSON.stringify(selectedrecords));
        }
    }

    public render() {
        this.rowSelected = this.rowSelected.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
        selectionSettings={this.settings} height={270} rowSelected={this.rowSelected} ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='150'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Touch interaction

When you tap a treegrid row on touchscreen device, the tapped row is selected.
It also shows a popup ![Multi Row selection](images/selection.jpg)  for multi-row selection.
To select multiple rows or cells, tap the popup![Multi Row or Cells](images/mselection.jpg)  and then tap the desired rows or cells.

> Multi-selection requires the selection [`type`](../api/treegrid/selectionSettings/#type) to be **Multiple**.

The following screenshot represents a treegrid touch selection in the device.

<!-- markdownlint-disable MD033 -->
<img src="../images/touch-selection.png" alt="Touch interaction" style="width:320px;height: 620px">
<!-- markdownlint-enable MD033 -->

## Multiple Selection based on condition

You can select multiple treegrid rows based on condition by using the [`selectRows`](../api/treegrid/#selectrows) method.

In the following code, the rows which contains *taskID* value as *3* and *5* are selected at initial rendering.

{% tab template="treegrid/selection", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public settings: SelectionSettingsModel = { type: 'Multiple' };

    public dataBound() {
        if (this.treegrid) {
          const rowIndexes : number[]=[];
          (this.treegrid.grid.dataSource as object[]).forEach((dat: any,index) => {
              if (dat.taskID === 3 || dat.taskID === 5) {
                rowIndexes.push(index);
              }
          });
          this.treegrid.selectRows(rowIndexes);
        }
      }

    public render() {
        this.dataBound = this.dataBound.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
        selectionSettings={this.settings} height={270} dataBound={this.dataBound} ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='150'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}