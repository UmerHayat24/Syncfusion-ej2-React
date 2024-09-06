---
title: "Clipboard"
component: "TreeGrid"
description: "Learn how to use the copy to clipboard functionality in the Essential JS 2 Tree Grid Control."
---

# Clipboard

The clipboard provides an option to copy selected rows or cells data into the clipboard.

The following list of keyboard shortcuts is supported in the Tree Grid to copy selected rows or cells data into the clipboard.

Interaction keys |Description
-----|-----
<kbd>Ctrl + C</kbd> |Copy selected rows or cells data into clipboard.
<kbd>Ctrl + Shift + H</kbd> |Copy selected rows or cells data with header into clipboard.

{% tab template="treegrid/clip-board", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: SelectionSettingsModel = { type: 'Multiple', mode: 'Row' };
    public pageSettings: PageSettingsModel = { pageSize: 10 };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true' pageSettings={this.pageSettings} selectionSettings={this.settings}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
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

## Copy to clipboard by external buttons

To copy selected rows or cells data into the clipboard with help of external buttons, you need to invoke the [`copy`](../api/treegrid/#copy) method.

{% tab template="treegrid/clip-board", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, TreeGrid, Inject, Page, TreeGridComponent, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}> {
  
  public treegrid: TreeGrid | null;
  public settings: SelectionSettingsModel = { type: 'Multiple', mode: 'Row' };
  public copy(){
    if (this.treegrid) {
      this.treegrid.copy();
    }
  }
  
  public copyHeader(){
    if (this.treegrid) {
      this.treegrid.copy(true);
    }
  }
  
  public render() {
    this.copy = this.copy.bind(this);
    this.copyHeader = this.copyHeader.bind(this);
    return (<div>
      <ButtonComponent onClick= { this.copy }>Copy</ButtonComponent>
      <ButtonComponent onClick= { this.copyHeader }>CopyHeader</ButtonComponent>
      <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
        ref={tree => this.treegrid = tree} allowPaging='true' selectionSettings={this.settings}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    </div>)
    }
}
```

{% endtab %}

## Copy Hierarchy Modes

Tree Grid provides support for a set of copy modes with [`copyHierarchyMode`](../api/treegrid/filterSettingsModel/#hierarchymode) property.
The below are the type of copy modes available in TreeGrid.

* **Parent** : This is the default copy hierarchy mode in Tree Grid. Clipboard value have the selected records with its parent records, if the selected records not have any parent record then the selected record will be in clipboard.

* **Child** : Clipboard value will have the selected records with its child record. If the selected records do not have any child record, then the selected records will be in clipboard.

* **Both** : Clipboard value will have the selected records with its both parent and child record. If the selected records do not have any parent and child record then the selected records alone in clipboard.

* **None** : Only the Selected records will be in clipboard.

{% tab template="treegrid/clip-board", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from "@syncfusion/ej2-react-dropdowns";
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-treegrid';
import { Inject, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    private treegrid: TreeGrid | null;
    private data: string[] = ['Parent', 'Child', 'Both', 'None']
    public settings: SelectionSettingsModel = { type: 'Multiple', mode: 'Row' };
    public onChange(sel: ChangeEventArgs): void {
        const mode: any = sel.value.toString();
        if (this.treegrid) {
            this.treegrid.copyHierarchyMode = mode;
        }
    }

    public render() {
        this.onChange = this.onChange.bind(this);
        return(
        <div>
        <DropDownListComponent popupHeight="250px" dataSource={this.data} value="Parent" change={this.onChange} width="150px" />
            <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='225' allowFiltering='true' selectionSettings={this.settings}
            ref={treegrid => this.treegrid = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='75' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
        </div>)
    }
}
```

{% endtab %}

## AutoFill

AutoFill Feature allows you to copy the data of selected cells and paste it to another cells by just dragging the autofill icon of the selected cells up to required cells. This feature is enabled by defining `enableAutoFill` property as true.

{% tab template="treegrid/clip-board", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent, Edit, Toolbar } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' };
    public settings: SelectionSettingsModel = { cellSelectionMode: 'Box', type: 'Multiple', mode: 'Cell'};
    public toolbarOptions: ToolbarItems[] = ['Add', 'Update', 'Cancel'];
    public pageSettings: PageSettingsModel = { pageSize: 10 };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true' enableAutoFill ='true' pageSettings={this.pageSettings} selectionSettings={this.settings} editSettings = {this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Edit, Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * If `enableAutoFill` is set to true, then the autofill icon will be displayed on cell selection to copy cells.
> * It requires the selection `mode` to be `Cell`,  `cellSelectionMode` to be `Box` and also Batch Editing should be enabled.

### Limitations of AutoFill

* Since the string values are not parsed to number and date type, so when the selected string type cells are dragged to number type cells then it will display as **NaN**. For date type cells, when the selected string type cells are dragged to date type cells then it will display as an **empty cell**.
* Linear series and the sequential data generations are not supported in this autofill feature.

## Paste

You can able to copy the content of a cell or a group of cells by selecting the cells and pressing <kbd>Ctrl + C</kbd> shortcut key and paste it to another set of cells by selecting the cells and pressing <kbd>Ctrl + V</kbd> shortcut key.

{% tab template="treegrid/clip-board", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent, Edit, Toolbar } from '@syncfusion/ej2-react-treegrid';
import { Page, SelectionSettingsModel, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' };
    public settings: SelectionSettingsModel = { cellSelectionMode: 'Box', type: 'Multiple', mode: 'Cell'};
    public toolbarOptions: ToolbarItems[] = ['Add', 'Update', 'Cancel'];
    public pageSettings: PageSettingsModel = { pageSize: 10 };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true' pageSettings={this.pageSettings} selectionSettings={this.settings} editSettings = {this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Edit, Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> To perform paste functionality, it requires the selection `mode` to be `Cell`,  `cellSelectionMode` to be `Box` and also Batch Editing should be enabled.

### Limitations of Paste Functionality

* Since the string values are not parsed to number and date type, so when the copied string type cells are pasted to number type cells then it will display as **NaN**. For date type cells, when the copied string format cells are pasted to date type cells then it will display as an **empty cell**.