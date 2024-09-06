---
title: "Editing"
component: "TreeGrid"
description: "Learn how to perform CRUD operations in various edit modes, and use different cell editors in the Essential JS 2 TreeGrid control."
---

# Editing

The TreeGrid component has options to dynamically insert, delete and update records.
Editing feature is enabled by using [`editSettings`](../api/treegrid/#editsettings) property and it requires a primary key column for CRUD operations.
To define the primary key, set [`columns.isPrimaryKey`](../api/treegrid/column/#isprimarykey) to **true** in particular column.

To get start quickly with CRUD functionalities, you can check on this video:
`youtube:JX8Ay-tH-WI`

To use CRUD, inject the [`Edit`](../api/treegrid/#editmodule) module in treegrid.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, EditSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell'
    };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='priority' headerText='Priority' width='90' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * You can disable editing for a particular column, by specifying
[`columns.allowEditing`](../api/treegrid/column/#allowediting) to **false**.

## Toolbar with edit option

The treegrid toolbar has the built-in items to execute Editing actions.
You can define this by using the [`toolbar`](../api/treegrid/#toolbar) property.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, EditSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Row'
    };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='priority' headerText='Priority' width='90' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Cell edit type and its params

The [`columns.editType`](../api/treegrid/column/#edittype) is used to customize the edit type of the particular column.
You can set the [`columns.editType`](../api/treegrid/column/#edittype) based on data type of the column.

* `numericedit` - [`NumericTextBox`](../numerictextbox) component for integers, double, and decimal data types.

* `defaultedit` - [`TextBox`](../textbox) component for string data type.

* `dropdownedit` - [`DropDownList`](../drop-down-list) component for list data type.

* `booleanedit` - [`CheckBox`](../check-box) component for boolean data type.

* `datepickeredit` - [`DatePicker`](../datepicker) component for date data type.

* `datetimepickeredit` - [`DateTimePicker`](../datetimepicker) component for date time data type.

Also, you can customize model of the [`columns.editType`](../api/treegrid/column/#edittype) component through the [`columns.edit.params`](../api/treegrid/column/#edit).

The following table describes cell edit type component and their corresponding edit params of the column.

Component |Example
-----|-----
[`NumericTextBox`](../numerictextbox) | params: { decimals: 2, value: 5 }
[`TextBox`](../textbox) | -
[`DropDownList`](../drop-down-list) | params: { value: 'Germany' }
[`Checkbox`](../check-box) | params: { checked: true}
[`DatePicker`](../datepicker) | params: { format:'dd.MM.yyyy' }
[`DateTimePicker`](../datetimepicker) | params: { value: new Date() }

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { IEditCell } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
    public format: any = {type:'dateTime', format:'M/d/y hh:mm a'};
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

    public datetimeParams: IEditCell = { params: { format: 'M/d/y hh:mm a' } };
    public numericParams: IEditCell = { params: { format: 'n' } };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270' editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='100' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' editType= 'stringedit'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='180' textAlign='Right' edit={this.datetimeParams} editType='datetimepickeredit' format={this.format} />
              <ColumnDirective field='approved' headerText='Approved' width='110' textAlign='Right' editType='booleanedit' type='boolean' displayAsCheckBox={true} />
              <ColumnDirective field='progress' headerText='Progress' textAlign='Right' width='120' editType='numericedit' edit={this.numericParams} />
              <ColumnDirective field='priority' headerText='Priority' width='110' editType='dropdownedit' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> If edit type is not defined in the column, then it will be considered as the *stringedit* type (Textbox component).

## Cell Edit Template

The cell edit template is used to add a custom component for a particular column by invoking the following functions:

* **create** - It is used to create the element at time of initialization.

* **write** - It is used to create custom component or assign default value at time of editing.

* **read** - It is used to read the value from component at time of save.

* **destroy** - It is used to destroy the component.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { AutoComplete } from '@syncfusion/ej2-dropdowns';
import { IEditCell } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Column, Edit, EditSettingsModel, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public elem: HTMLElement;
    public autoCompleteobj: AutoComplete;
    public treegridObj: TreeGrid | null;

    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell', newRowPosition: 'Below' };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];

    public editTemplate : IEditCell = {
        create:()=>{
            this.elem = document.createElement('input');
            return this.elem;
        },
        destroy:()=>{
            this.autoCompleteobj.destroy();
        },
        read:()=>{
            return this.autoCompleteobj.value;
        },
        write:(args:{rowData: object, column: Column})=>{
            if (this.treegridObj) {
                this.autoCompleteobj = new AutoComplete({
                    dataSource: new DataManager(this.treegridObj.grid.dataSource as object[]),
                    fields: { value: 'taskName' },
                    value: args.rowData[args.column.field]
                });
                this.autoCompleteobj.appendTo(this.elem);
            }
    }};


    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            height='400' editSettings={this.editOptions} toolbar={this.toolbarOptions}
            ref={treegrid=> this.treegridObj = treegrid}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='100' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' editType= 'stringedit' edit={this.editTemplate}/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Edit Modes

TreeGrid supports the following types of edit modes, they are:

* Cell
* Row
* Dialog
* Batch

### Cell

In Cell edit mode, when you double click on a cell, it is changed to edit state.
You can change the cell value and save to the data source.
To enable Cell edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as **Cell**.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell',
        newRowPosition: 'Below'
    };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
             height='270' editSettings={this.editOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> Cell edit mode is default mode of editing.

### Row

In Row edit mode, when you start editing the currently selected record, the entire row is changed to edit state.
You can change the cell values of the row and save edited data to the data source.
To enable Row edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as **Row**.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Row'
    };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
             height='270' editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Dialog

In Dialog edit mode, when you start editing the currently selected row, data will be shown on a dialog.
You can change the cell values and save edited data to the data source.
To enable Dialog edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as **Dialog**.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Dialog'
    };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='270' editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Batch

In Batch edit mode, when you double-click on the treegrid cell, the target cell goes into edit state.
You can bulk save (added, changed and deleted data in the single request) to data source by clicking on the toolbar's **Update** button or by externally invoking the [`batchSave`](../api/treegrid/#batchsave) method.
To enable Batch edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as **Batch**.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Batch',
    };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Update', 'Cancel'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
             height='270' editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Dialog template

The dialog template editing provides an option to customize the default behavior of dialog editing. Using the dialog template, you can render your own editors by defining the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as **Dialog** and [`template`](../api/treegrid/editSettingsModel/#template) as SCRIPT element ID or HTML string which holds the template.

In some cases, you need to add the new field editors in the dialog which are not present in the column model. In that situation, the dialog template will help you to customize the default edit dialog.

For quick details with dialog template, you can check on this video:
`youtube:dOi4iNIf5M8`

In the following sample, treegrid enabled with dialog template editing.

{% tab template="treegrid/dialogtemplate", sourceFiles="app/App.tsx,app/template.tsx,app/orderModel.tsx", compileJsx=true %}

```typescript
import { setValue } from '@syncfusion/ej2-base';
import { DialogEditEventArgs } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';
import { IOrderModel } from './orderModel';
import { DialogFormTemplate } from './template';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Dialog',
        template: this.dialogTemplate.bind(this)
    };

    public dialogTemplate(props: IOrderModel): any {
        const obj = [props, this.treegrid];
        return (<DialogFormTemplate {...obj} />);
    }
    public actionComplete(args: DialogEditEventArgs) {
       if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
           // Add Validation Rules
            const form: HTMLFormElement = args.form as HTMLFormElement;
            form.ej2_instances[0].addRules('progress', {max: 100});
            if (args.requestType === 'beginEdit') {
                (form.elements.namedItem('taskName') as HTMLInputElement).focus();
            }
       }
    }

    public actionBegin (args: DialogEditEventArgs) {
        if (args.requestType === 'save') {
            // cast string to integer value.
            const val: string = ((args.form as HTMLFormElement)
                .querySelector("#progress") as HTMLInputElement).value;
            setValue('data.progress', parseFloat(val), args);
        }
    }

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
             editSettings={this.editOptions} toolbar={this.toolbarOptions} ref={g=> this.treegrid = g}
              actionBegin={this.actionBegin} actionComplete={this.actionComplete}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> The template form editors should have **name** attribute.

### Template Context

The template should be a React Component class. You can access the row information inside the Component class using *props*, you can bind the attribute or value based on this row information.

The following properties will be available at the time of template execution.

| Property Name | Usage |
|---------------|-------|
| <kbd>isAdd</kbd> | A Boolean property; it defines whether the current row should be a new record or not. |

In the following code example, the *OrderID* textbox has been disabled by using the **isAdd** property.

```html
// The disabled attributes will be added based on the isAdd property.
<input id="taskID" name="taskID" type="text" disabled={!data.isAdd} value={data.taskID} onChange={this.onChange} />

```

The following code example illustrates rendering the *taskID* textbox, when a new record is added.

### Get value from editor

You can read, format, and update the current editor value in the [`actionBegin`](../api/treegrid/#actionbegin) event at the time of setting **requestType** to **save**.

In the following code example, the *progress* value has been formatted and updated.

``` typescript
    public actionBegin (args: DialogEditEventArgs) {
        if (args.requestType === 'save') {
            // cast string to integer value.
            const val: string = ((args.form as HTMLFormElement)
                .querySelector("#progress") as HTMLInputElement).value;
            setValue('data.progress', parseFloat(val), args);
        }
    }

```

### Set focus to editor

By default, the first input element in the dialog will be focused while opening the dialog.
If the first input element is in disabled or hidden state, focus the valid input element in the
[`actionComplete`](../api/treegrid/#actioncomplete) event based on **requestType** as *beginEdit*.

```typescript

    public actionComplete(args: DialogEditEventArgs) {
       if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            const form: HTMLFormElement = args.form as HTMLFormElement;
            if (args.requestType === 'beginEdit') {
                (form.elements.namedItem('taskName') as HTMLInputElement).focus();
            }
       }
    }

```

### Adding validation rules for custom editors

If you have used additional fields that are not present in the column model, then add the validation rules to them in the [`actionComplete`](../api/treegrid/#actioncomplete) event.

```typescript

    public actionComplete(args: DialogEditEventArgs) {
       if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
           // Add Validation Rules
            const form: HTMLFormElement = args.form as HTMLFormElement;
            form.ej2_instances[0].addRules('progress', {max: 100});
       }
    }


```

## Adding row position

The TreeGrid control provides the support to add the new row in the top, bottom, above selected row, below selected row and child position of tree grid content using [`editSettings.newRowPosition`](../api/treegrid/editSettingsModel/#newrowposition) property. By default, a new row will be added at the top of the treegrid.

The following examples shows how to set new row position as *Child* in tree grid.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell',
        newRowPosition: 'Child'
    };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Command column

The command column provides an option to add CRUD action buttons in a column. This can be defined by the [`column.commands`](../api/treegrid/column/#commands) property.

The available built-in command buttons are:

| Command Button | Actions |
|----------------|---------|
| Edit | Edit the current row.|
| Delete | Delete the current row.|
| Save | Update the edited row.|
| Cancel | Cancel the edited state. |

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { CommandModel } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { CommandColumn, Edit, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public commands: CommandModel[] = [
        {
            buttonOption: { cssClass: 'e-flat', iconCss: 'e-edit e-icons' },
            type: 'Edit',
        },
        {
            buttonOption: { cssClass: 'e-flat', iconCss: 'e-delete e-icons' },
            type: 'Delete'
        },
        {
            buttonOption: { cssClass: 'e-flat', iconCss: 'e-update e-icons' },
            type: 'Save'
        },
        {
            buttonOption: { cssClass: 'e-flat', iconCss: 'e-cancel-icon e-icons' },
            type: 'Cancel'
        }
    ];
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Row'
    };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective headerText='Manage Records' width='130' commands= {this.commands}/>
            </ColumnsDirective>
            <Inject services={[Edit,CommandColumn]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Custom command

 The custom command buttons can be added in a column by using the [`column.commands`](../api/treegrid/column/#commands) property and
the action for the custom buttons can be defined in the [`buttonOption.click`](../api/grid/commandButtonOptions/#click) event.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { closest } from '@syncfusion/ej2-base';
import { Column, CommandModel, Row } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { CommandColumn, Edit, EditSettingsModel, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowDeleting: true };
    public commands: CommandModel[] = [
      {
        buttonOption: {
          click: this.onClick.bind(this),
          content: 'Details', cssClass: 'e-flat'
        }
      }
    ];
    public treegrid: TreeGrid | null;
  
    public onClick(args: Event): void  {
      if (this.treegrid) {
        const rowObj: Row<Column> =
          this.treegrid.grid.getRowObjectFromUID(closest(args.target as Element, '.e-row')
          .getAttribute('data-uid') as string);
        const rowData: object = rowObj.data as object;
        alert(JSON.stringify(rowData));
      }
    }

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} ref={g=> this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective headerText='Commands' width='120' commands= {this.commands}/>
            </ColumnsDirective>
            <Inject services={[Edit,CommandColumn]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Confirmation messages

### Delete confirmation

The delete confirm dialog can be shown when deleting a record by defining the [`showDeleteConfirmDialog`](../api/treegrid/editSettingsModel/#showdeleteconfirmdialog) as **true**

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell',
        showDeleteConfirmDialog: true
    };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='130' format='yMd' textAlign='Right' type='date' editType='datepickeredit' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> The [`showDeleteConfirmDialog`](../api/treegrid/editSettingsModel/#showdeleteconfirmdialog) supports all type of edit modes.

## Column validation

Column validation allows you to validate the edited or added row data and it display errors for invalid fields before saving data. TreeGrid uses **Form Validator** component for column validation.
You can set validation rules by defining the [`columns.validationRules`](../api/treegrid/column/#validationrules).

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { IEditCell } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell',
        showDeleteConfirmDialog: true
    };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];

    public format: any = {type:'dateTime', format:'M/d/y hh:mm a'};

    public datetimeParams: IEditCell = { params: { format: 'M/d/y hh:mm a' } };
    public numericParams: IEditCell = { params: { format: 'n' } };

    public taskIDRules: object = { required: true, number: true };
    public progressRules: object = { number: true, min: 0 };
    public startDateRules: object = { date: true };
    public priorityRules: object = { required: true };
    public taskNameRules: object = { required: true };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true} validationRules={this.taskIDRules}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' validationRules={this.taskNameRules}/>
              <ColumnDirective field='startDate' headerText='Start Date' width='150' textAlign='Right' edit={this.datetimeParams}
               editType='datetimepickeredit' format={this.format} validationRules={this.startDateRules} />
              <ColumnDirective field='approved' headerText='Approved' width='110' textAlign='Right' editType='booleanedit' type='boolean' displayAsCheckBox={true} />
              <ColumnDirective field='progress' headerText='Progress' textAlign='Right' width='120' editType='numericedit' edit={this.numericParams} validationRules={this.progressRules} />
              <ColumnDirective field='priority' headerText='Priority' width='110' editType='dropdownedit' validationRules={this.priorityRules} />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Custom validation

You can define your own custom validation rules for the specific columns by using **Form Validator custom rules**.

In the below demo, custom validation applied for *Priority* column.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell'
    };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];
    public priorityRules: object = {
        minLength: [this.customFn, 'Value should be within 8 letters'],
        required: true
    };
    public customFn(args: { [key: string]: string }) : boolean {
        return getValue('value', args) <= 8;
    };


    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270' editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' textAlign='Right' editType='datepickeredit' format='yMd' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='110' validationRules={this.priorityRules} />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Persisting data in server

Edited data can be persisted in the database using the RESTful web services.

All the CRUD operations in the treegrid are done through [`DataManager`](../data). The `DataManager` has an option to bind all the CRUD related data in server-side.

> For your information, the ODataAdaptor persists data in the server as per OData protocol.

In the following section, we have explained how to perform CRUD operation in server-side using the [`UrlAdaptor`](../../data/adaptors.html#url-adaptor) and `RemoteSave Adaptor`.

### URL adaptor

You can use the [`UrlAdaptor`](../../data/adaptors.html#url-adaptor) of `DataManager` when binding data source from remote data.
In the initial load of treegrid, data are fetched from remote data and bound to the treegrid using `url` property of `DataManager`.
You can map The CRUD operation in treegrid can be mapped to server-side Controller actions using the properties `insertUrl`, `removeUrl`, `updateUrl` and `batchUrl`.

The following code example describes the above behavior.

```typescript

import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';

export default class App extends React.Component<{}, {}>{

    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row', newRowPosition: 'Below' };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

    public dataManager: DataManager = new DataManager({
        adaptor: new UrlAdaptor,
        insertUrl: "Home/Insert",
        removeUrl: "Home/Delete",
        updateUrl: "Home/Update",
        batchUrl: "Home/Remove",
        url: "Home/DataSource",
    });

    public render() {
        return <TreeGridComponent dataSource={this.dataManager} treeColumnIndex={1} idMapping= 'TaskID'
        parentIdMapping='parentID' height='270' editSettings={this.editOptions}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='StartDate' headerText='Start Date' width='90' textAlign='Right' editType='datepickeredit' format='yMd' type='date' />
              <ColumnDirective field='EndDate' headerText='End Date' width='90' format='yMd' textAlign='Right' />
              <ColumnDirective field='Priority' headerText='Priority' width='110' editType='dropdownedit'/>
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}

```

Also, when using the `UrlAdaptor`, you need to return the data as JSON from the controller action and the JSON object must contain a property as `result` with dataSource as its value and one more property `count` with the dataSource total records count as its value.

The following code example describes the above behavior.

```typescript

public ActionResult DataSource(DataManager dm)
{
    var DataSource = TreeData.GetTree();
    DataOperations operation = new DataOperations();
    if (dm.Where != null && dm.Where.Count > 0)
    {
        DataSource = operation.PerformFiltering(DataSource, dm.Where, "and");   //perform filtering  and maintain child records on Expand/Collapse operation
    }
    var count = DataSource.ToList<TreeData>().Count();
    if (dm.Skip != 0)
    {
        DataSource = operation.PerformSkip(DataSource, dm.Skip);   //Paging
    }
    if (dm.Take != 0)
    {
        DataSource = operation.PerformTake(DataSource, dm.Take);
    }
    return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
}

```

### Insert record

Using the `insertUrl` property, you can specify the controller action mapping URL to perform insert operation on the server-side.

The following code example describes the above behavior and also we have inserted new record based on the newRowPosition TreeGrid editSettings as "Below".

```typescript

public void Insert(TreeGridData value, int relationalKey)
{
    var i = 0;
    for (; i < TreeData.tree.Count; i++)
    {
        if (TreeData.tree[i].TaskID == relationalKey)
        {
            break;
        }
    }
    i += FindChildRecords(relationalKey); // Inserted new record when newRowPosition API is in "Below".
    TreeData.tree.Insert(i + 1, value);
}

public int FindChildRecords(int id)
{
    var count = 0;
    for (var i = 0; i < TreeData.tree.Count; i++)
    {
        if (TreeData.tree[i].ParentItem == id)
        {
            count++;
            count += FindChildRecords(TreeData.tree[i].TaskID);
        }
    }
    return count;
}

```

The newly added record details are bound to the `value` parameter and `relationalKey` contains primaryKey value of an selected record helps to find out the position of newly added record. Please refer to the following screenshot.

![Insert](images/insert.PNG)

### Update record

Using the `updateUrl` property, the controller action mapping URL can be specified to perform save/update operation on the server-side.

The following code example describes the previous behavior.

```typescript

public ActionResult Update(TreeGridData value)
{
    var val = TreeData.tree.Where(ds => ds.TaskID == value.TaskID).FirstOrDefault();
    val.TaskName = value.TaskName;
    val.StartDate = value.StartDate;
    val.Duration = value.Duration;
    val.Priority = value.Priority;
    val.Progress = value.Progress;
    return Json(value);
}

```

The updated record details are bound to the `value` parameter. Please refer to the following screenshot.

![Update](images/update.PNG)

### Delete record

Using the `removeUrl` and `batchUrl` property, the controller action mapping URL can be specified to perform delete operation on the server-side.

The following code example describes the previous behavior.

```typescript

public ActionResult Delete(int key)
{
    TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == key).FirstOrDefault());
}

// Remove method (batchUrl) will be triggered when we delete parent record.

public ActionResult Remove(List<TreeGridData> changed, List<TreeGridData> added, List<TreeGridData> deleted)
{
    for (var i = 0; i < deleted.Count; i++)
    {
        TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == deleted[i].TaskID).FirstOrDefault());
    }
}

```

The deleted record primary key value is bound to the `key` parameter. Please refer to the following screenshot.

![Delete](images/remove.PNG)

While delete parent record, the parent and child records is bound to the `deleted` parameter. Please refer to the following screenshot.

![Remove](images/delete.PNG)

### Remote Save Adaptor

You may need to perform all Tree Grid Actions in client-side except the CRUD operations, that should be interacted with server-side to persist data. It can be achieved in TreeGrid by using **RemoteSaveAdaptor**.

Datasource must be set to **json** property and set **RemoteSaveAdaptor** to the **adaptor** property. CRUD operations can be mapped to server-side using **updateUrl**, **insertUrl**, **removeUrl** and **batchUrl** properties.

You can use the following code example to use **RemoteSaveAdaptor** in TreeGrid.

```typescript

import { DataManager, RemoteSaveAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { projectData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row', newRowPosition: 'Below' };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

    public dataManager: DataManager = new DataManager({
        adaptor: new RemoteSaveAdaptor,
        insertUrl: "Home/Insert",
        removeUrl: "Home/Delete",
        updateUrl: "Home/Update",
        batchUrl: "Home/Remove",
        json: projectData,
    });

    public render() {
        return <TreeGridComponent dataSource={this.dataManager} treeColumnIndex={1} idMapping= 'TaskID'
        parentIdMapping='parentID' height='270' editSettings={this.editOptions}
        toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='StartDate' headerText='Start Date' width='90' textAlign='Right' editType='datepickeredit' format='yMd' type='date' />
              <ColumnDirective field='EndDate' headerText='End Date' width='90' format='yMd' textAlign='Right' />
              <ColumnDirective field='Priority' headerText='Priority' width='110' editType='dropdownedit'/>
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}

```

The following code example describes the CRUD operations handled at server-side.

```typescript

public void Insert(TreeData value, int relationalKey)
{
    var i = 0;
    for (; i < TreeData.tree.Count; i++)
    {
        if (TreeData.tree[i].TaskID == relationalKey)
        {
            break;
        }
    }
    i += FindChildRecords(relationalKey); // Inserted new record when newRowPosition API is in "Below".
    TreeData.tree.Insert(i + 1, value);
}

public ActionResult Update(TreeData value)
{
    var val = TreeData.tree.Where(ds => ds.TaskID == value.TaskID).FirstOrDefault();
    val.TaskName = value.TaskName;
    val.StartDate = value.StartDate;
    val.Duration = value.Duration;
    val.Priority = value.Priority;
    val.Progress = value.Progress;
    return Json(value);
}

public ActionResult Delete(int key)
{
    TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == key).FirstOrDefault());;
}

// Remove method (batchUrl) will be triggered when we delete parent record.

public ActionResult Remove(List<TreeGridData> changed, List<TreeGridData> added, List<TreeGridData> deleted)
{
    for (var i = 0; i < deleted.Count; i++)
    {
        TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == deleted[i].TaskID).FirstOrDefault());
    }
}

```

## Default column values on add new

The treegrid provides an option to set the default value for the columns when adding a new record in it.
To set a default value for the particular column by defining the [`columns.defaultValue`](../api/treegrid/column/#defaultvalue).

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell'
    };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' textAlign='Right' editType='datepickeredit' format='yMd' type='date' />
              <ColumnDirective field='priority' headerText='Priority' width='110' editType='dropdownedit' defaultValue='Normal' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Disable editing for particular column

You can disable editing for particular columns by using the [`columns.allowEditing`](../api/treegrid/column/#allowediting).

In the following demo, editing is disabled for the *Start Date* column.

{% tab template="treegrid/editing", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Edit, EditSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell'
    };

    public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270'
         editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' allowEditing={false} textAlign='Right' editType='datepickeredit' format='yMd' type='date' />
              <ColumnDirective field='priority' headerText='Priority' width='110' editType='dropdownedit' />
            </ColumnsDirective>
            <Inject services={[Edit,Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Troubleshoot: Editing works only for first row

The Editing functionalities can be performed based upon the primary key value of the selected row.
If [`column.primaryKey`](../api/treegrid/column/#isprimarykey) is not defined in the treegrid, then edit or delete action take places the first row.
