---
title: "How To"
component: "Grid"
description: "Learn how to refresh the datasource, exporting filtered data, enable and disable grid actions, customize the pager dropdown in Essential JS 2 DataGrid."
---

# How To

## How to Refresh the Datasource

You can add/delete the datasource records through an external button. To reflect the datasource changes in grid,
you need to invoke the [`refresh`](../api/grid/#refresh) method.

Please follow the below steps to refresh the grid after datasource change.

**Step 1**:

Add/delete the datasource record by using the following code.

```typescript
    this.grid.dataSource.unshift(data); // Add a new record.

    this.grid.dataSource.splice(selectedRow, 1); // Delete a record.

```

**Step 2**:

Refresh the grid after the datasource change by using the [`refresh`](../api/grid/#refresh) method.

```typescript
    this.grid.refresh(); // Refresh the Grid.

```

{% tab template="grid/change-headertext", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public data: Object[] = data;
    private grid: GridComponent;
    public add() {
        let data: Object = { OrderID: 10247, CustomerID: "ASDFG", ShipCity: 'Vins et alcools Chevalier' , ShipName: 'Reims' };
        this.grid.dataSource.unshift(data); // Add record.
        this.grid.refresh(); // Refresh the Grid.
    }
    public delete() {
        let selectedRow: number = this.grid.getSelectedRowIndexes()[0];
        if (this.grid.getSelectedRowIndexes().length){
            this.grid.dataSource.splice(selectedRow, 1); //Delete record.
        }
        else {
            alert("No records selected for delete operation");
        }
        this.grid.refresh(); // Refresh the Grid.
    }
    render() {
        return (<div>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.add.bind(this)}>Add</ButtonComponent>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.delete.bind(this)}>Delete</ButtonComponent>
            <GridComponent dataSource={this.data} height={280} ref={g => this.grid = g}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'></ColumnDirective>
                </ColumnsDirective>
            </GridComponent>
        </div>)
    }
}
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

## Enable/Disable Grid and its actions

You can enable/disable the Grid and its actions by applying/removing corresponding CSS styles.

To enable/disable the grid and its actions, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .disablegrid {
        pointer-events: none;
        opacity: 0.4;
    }
    .wrapper {
        cursor: not-allowed;
    }

```

**Step 2**:

Add/Remove the CSS class to the Grid in the click event handler of Button.

```typescript
    btnClick(): void {
        if (this.Grid.element.classList.contains('disablegrid')) {
            this.Grid.element.classList.remove('disablegrid');
            document.getElementById("GridParent").classList.remove('wrapper');
        }
        else {
            this.Grid.element.classList.add('disablegrid');
            document.getElementById("GridParent").classList.add('wrapper');
        }
    }

```

In the below demo, the button click will enable/disable the Grid and its actions.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowAdding:true, allowEditing: true, allowDeleting:true };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    private Grid: GridComponent;

    btnClick(): void {
        if (this.Grid.element.classList.contains('disablegrid')) {
            this.Grid.element.classList.remove('disablegrid');
            document.getElementById("GridParent").classList.remove('wrapper');
        }
        else {
            this.Grid.element.classList.add('disablegrid');
            document.getElementById("GridParent").classList.add('wrapper');
        }
    }

    render() {
        return (
            <div>
            <ButtonComponent cssClass='e-flat e-primary' ref={(scope) => { this.btnobj = scope; }} iconCss='e-icons e-play-icon'
                            isToggle onClick={ this.btnClick.bind(this) }>Enable/Disable Grid</ButtonComponent>
            <div id="GridParent">
            <GridComponent dataSource={data} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265} ref={(scope) => { this.Grid = scope; }}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                    <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[Edit, Toolbar]} />
            </GridComponent></div></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

## Columns

### How to Change Column Header Text Dynamically

You can change the column [`headerText`](../api/grid/column/#headertext) dynamically through an external button.

Follow the given steps to change the header text dynamically:

**Step 1**:

Get the column object corresponding to the field name by using the [`getColumnByField`](../api/grid/#getcolumnbyfield) method.
Then change the header Text value.

```typescript
let column = this.grid.getColumnByField("ShipCity"); // Get column object.
column.headerText = 'Changed Text';

```

**Step 2**:

To reflect the changes in the grid header, invoke the [`refreshHeader`](../api/grid/#refreshheader) method.

```typescript
this.grid.refreshHeader();

```

{% tab template="grid/change-headertext", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public data: Object[] = data;
    private grid: GridComponent;
    public click() {
        let column = this.grid.getColumnByField("ShipCity");//get the JSON object of the column corresponding to the field name
        column.headerText = "Changed Text" // assign a new header text to the column
        this.grid.refreshHeader();
    }
    render() {
        return (<div>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.click.bind(this)}>Change Header Text</ButtonComponent>
            <GridComponent dataSource={this.data} height={280} ref={g => this.grid = g}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'></ColumnDirective>
                </ColumnsDirective>
            </GridComponent>
        </div>)
    }
}
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Customize Column Styles

You can customise the appearance of header and content of the particular column using the
[`customAttributes`](../api/grid/column/#customattributes) property.

To customize the grid column, follow the given steps:

**Step 1**:

Create a css class with custom style to override the default style for rowcell and headercell.

```css
.e-grid .e-rowcell.customcss{
    background-color: #ecedee;
    font-family: 'Bell MT';
    color: 'red';
    font-size: '20px';
}

.e-grid .e-headercell.customcss{
    background-color: #2382c3;
    color: white;
    font-family: 'Bell MT';
    font-size: '20px';
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../api/grid/column/#customattributes) property.

```typescript
<ColumnDirective field='CustomerID' width='130' customAttributes={this.customAttributes}></ColumnDirective>

```

{% tab template="grid/custom-column", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public customAttributes: Object = {class: 'customcss'};
    render() {
        return <GridComponent dataSource={data} height={320}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' width='100' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' width='130' customAttributes={this.customAttributes}></ColumnDirective>
                    <ColumnDirective field='EmployeeID' width='100' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='ShipCountry' width='100'></ColumnDirective>
                </ColumnsDirective>
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Custom Tooltip for columns

You can achieve the custom tooltip([`EJ2 Tooltip`](../../../tooltip/getting-started/)) for Grid by using the
[`queryCellInfo`](../api/grid/#querycellinfo) event.

Render the ToolTip component for the grid cells by using the following code in the
[`queryCellInfo`](../api/grid/#querycellinfo) event.

```typescript
public tooltip(args){
    let tooltip: Tooltip = new Tooltip({
        content: args.data[args.column.field].toString()
    }, args.cell);
}

```

{% tab template="grid/custom-tooltip", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Tooltip } from '@syncfusion/ej2-popups';
import { Grid, GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{

    public tooltip(args){
        let tooltip: Tooltip = new Tooltip({
        content: args.data[args.column.field].toString()
        }, args.cell);
    }

    render() {
        return (<div>
        <GridComponent dataSource={data} height={315} queryCellInfo={this.tooltip.bind(this)} >
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'></ColumnDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='100' format="C2" textAlign="Right"></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'></ColumnDirective>
            </ColumnsDirective>
        </GridComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### How to change the Orientation of Header Text

You can change the orientation of the header text by using the [`customAttributes`](../api/grid/column/#customattributes) property.

Ensure the following steps:

**Step 1**:

Create a css class with orientation style for grid header cell.

```css
.orientationcss .e-headercelldiv {
    transform: rotate(90deg);
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../api/grid/column/#customattributes) property.

```typescript
    <ColumnDirective field='Freight' headerText='Freight' customAttributes={this.customAttributes} width='80' format="C2" textAlign="Center"></ColumnDirective>

```

**Step 3**:

Resize the header cell height by using the following code.

```typescript
public setHeaderHeight(args) {
    let textWidth: number = document.querySelector(".orientationcss > div").scrollWidth;//Obtain the width of the headerText content.
    let headerCell: NodeList = document.querySelectorAll(".e-headercell");
    for(let i: number = 0; i < headerCell.length; i++) {
        (headerCell.item(i)).style.height = textWidth + 'px'; //Assign the obtained textWidth as the height of the headerCell.
    }
}

```

{% tab template="grid/header-orientation", sourceFiles="app/**/*.tsx, index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Grid, GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    private customAttributes: Object = { class: 'orientationcss'};
    public setHeaderHeight(args) {
        let textWidth: number = document.querySelector(".orientationcss > div").scrollWidth;//Obtain the width of the headerText content.
        let headerCell: NodeList = document.querySelectorAll(".e-headercell");
        for(let i: number = 0; i < headerCell.length; i++) {
            (headerCell.item(i)).style.height = textWidth + 'px'; //Assign the obtained textWidth as the height of the headerCell.
        }
    }

    render() {
        return (<div>
        <GridComponent dataSource={data} height={260} created={this.setHeaderHeight.bind(this)} >
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'></ColumnDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' customAttributes={this.customAttributes} width='80' format="C2" textAlign="Center"></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'></ColumnDirective>
            </ColumnsDirective>
        </GridComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Render React Component in column

You can use [`queryCellInfo`](../api/grid/#querycellinfo) event to render the React component inside Grid cells.
In the following sample, the DropDownList is rendered in the `ShipCountry` column

{% tab template="grid/dropdown-component", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Tooltip } from '@syncfusion/ej2-popups';
import { Grid, GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
  public fields:{[key:string]:string}={value:"ShipCountry",text:"ShipCountry"}
  public value: string = 'Germany';

  public dropdown(args) {
    if(args.column.field == "ShipCountry"){
       ReactDOM.render( <DropDownListComponent id="dropdown" fields={this.fields} value={this.value} dataSource={data} change={this.onChange.bind(this)}/>,args.cell)
       }
    }
   public onChange(args){
   //Event will trigger when you have change the value in dropdown column
   alert(args.value)
   }

    render() {
        return (<div>
        <GridComponent dataSource={data} height={315} queryCellInfo={this.dropdown.bind(this)} >
            <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'></ColumnDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
             </ColumnsDirective>
        </GridComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Customize the icon for column menu

You can customize the column menu icon by overriding the default grid class `.e-icons.e-columnmenu` with a custom property `content` as mentioned below,

```css
.e-grid .e-columnheader .e-icons.e-columnmenu::before {
              content: "\e941";
      }
```

In the below sample, grid is rendered with a customized column menu icon.

{% tab template="grid/custom-column-menu-icon", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Grid, GridComponent, ColumnsDirective, ColumnDirective, ColumnMenu, Inject } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{

    render() {
        return (<div>
        <GridComponent dataSource={data} height={315} showColumnMenu={true} >
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100'></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'></ColumnDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='100' format="C2"></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[ColumnMenu]} />
        </GridComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

## Editing

### Customize the Edit Dialog

You can customize the appearance of the edit dialog in the [`actionComplete`](../api/grid/#actioncomplete) event based on `requestType` as `beginEdit` or `add`.

In the below example, we have changed the dialog's header text for editing and adding records.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];

    actionComplete(args: DialogEditEventArgs): void {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            let dialog: Dialog = args.dialog;
            dialog.height = 400;
            // change the header of the dialog
            dialog.header = args.requestType === 'beginEdit' ? 'Record of ' + args.rowData['CustomerID'] : 'New Customer';
        }
    }

    render() {
        return <GridComponent dataSource={data} actionComplete={this.actionComplete.bind(this)} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Show or Hide columns in Dialog editing

You can show hidden columns or hide visible column's editor in the dialog while editing the grid record using [`actionBegin`](../api/grid/#actionbegin) and [`actionComplete`](../api/grid/#actioncomplete) events.

In the `actionBegin` event, based on `requestType` as `beginEdit` or  `add`. We can show or hide the editor by using `column.visible` property.

In the `actionComplete` event, based on `requestType` as `save`. We can reset the properties back to the column state.

In the below example, we have rendered the grid columns `CustomerID` as hidden column and `ShipCountry` as visible column. In the edit mode, we have changed the `CustomerID` column to visible state and `ShipCountry` column to hidden state.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
    private grid: GridComponent;

    actionBegin(args: DialogEditEventArgs): void {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            for (var i = 0; i < this.grid.columns.length; i++) {
                if (this.grid.columns[i].field == "CustomerID") {
                    this.grid.columns[i].visible = true;
                }
                else if (this.grid.columns[i].field == "ShipCountry") {
                    this.grid.columns[i].visible = false;
                }
            }
        }
    }
    actionComplete(args: DialogEditEventArgs): void {
        if (args.requestType === 'save') {
            for (var i = 0; i < this.grid.columns.length; i++) {
                if (this.grid.columns[i].field == "CustomerID") {
                    this.grid.columns[i].visible = false;
                }
                else if (this.grid.columns[i].field == "ShipCountry") {
                    this.grid.columns[i].visible = true;
                }
            }
        }
    }

    render() {
        return <GridComponent dataSource={data} actionBegin={this.actionBegin.bind(this)} actionComplete={this.actionComplete.bind(this)} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265} ref={g => this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120' visible={false}></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2' editType='numericedit'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Cascading DropDownList with Grid editing

You can achieve the Cascading DropDownList with grid Editing by using the Cell Edit Template feature.

In the below demo, Cascading DropDownList rendered for `ShipCountry` and `ShipState` column.

{% tab template="grid/editing", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
 EditSettingsModel, ToolbarItems, IEditCell } from '@syncfusion/ej2-react-grids';
import { cascadeData  } from './datasource';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public countryParams : IEditCell = {
        create:()=>{
            this.countryElem = document.createElement('input');
                return this.countryElem;
            },
            read:()=>{
                return this.countryObj.text;
            },
            destroy:()=>{
                this.countryObj.destroy();
            },
            write:()=>{
                this.countryObj = new DropDownList({
                dataSource: this.country,
                fields: { value: 'countryId', text: 'countryName' },
                change: () => {
                this.stateObj.enabled = true;
                let tempQuery: Query = new Query().where('countryId', 'equal', this.countryObj.value);
                this.stateObj.query = tempQuery;
                this.stateObj.text = null;
                this.stateObj.dataBind();
            },
            placeholder: 'Select a country',
            floatLabelType: 'Never'
            });
            this.countryObj.appendTo(this.countryElem);
    }};
    public stateParams : Object = {
            create:()=>{
                this.stateElem = document.createElement('input');
                return this.stateElem;
            },
            read:()=>{
                return this.stateObj.text;
            },
            destroy:()=>{
                this.stateObj.destroy();
            },
            write:()=>{
                this.stateObj = new DropDownList({
                dataSource: this.stateColl,
                fields: { value: 'stateId', text: 'stateName' },
                enabled: false,
                placeholder: 'Select a state',
                floatLabelType: 'Never'
            });
            this.stateObj.appendTo(this.stateElem);
    }};

    public countryElem : HTMLElement;
    public countryObj : DropDownList;

    public stateElem : HTMLElement;
    public stateObj : DropDownList;

    public country: { [key: string]: Object }[] = [
        { countryName: 'United States', countryId: '1' },
        { countryName: 'Australia', countryId: '2' }
    ];
    public stateColl: { [key: string]: Object }[] = [
        { stateName: 'New York', countryId: '1', stateId: '101' },
        { stateName: 'Virginia ', countryId: '1', stateId: '102' },
        { stateName: 'Washington', countryId: '1', stateId: '103' },
        { stateName: 'Queensland', countryId: '2', stateId: '104' },
        { stateName: 'Tasmania ', countryId: '2', stateId: '105' },
        { stateName: 'Victoria', countryId: '2', stateId: '106' }
    ];

    render() {
        return <GridComponent dataSource={cascadeData } editSettings={this.editOptions} toolbar={this.toolbarOptions} height={273}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150' editType= 'dropdownedit' edit={this.countryParams} textAlign="Right"></ColumnDirective>
                <ColumnDirective field='ShipState' headerText='Ship State' editType= 'dropdownedit' edit={this.stateParams} width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Provide custom data source and enabling filtering to DropDownList

You can provide data source to the DropDownList by using the `columns.edit.params` property.

While setting new data source using edit params, you must specify a new `query` property too for the DropDownList as follows,

```typescript
public countryParams : IEditCell = {
        params:   {
            allowFiltering: true,
            dataSource: this.country,
            fields: { text: "countryName", value: "countryName"},
            query: new Query(),
            actionComplete: () => false
            }
        };
```

You can also enable filtering for the DropDownList by passing the `allowFiltering` as `true` to the edit params.

In the below demo, DropDownList is rendered with custom Datasource for the `ShipCountry` column and enabled filtering to search DropDownList items.

{% tab template="grid/editing", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
 EditSettingsModel, ToolbarItems, IEditCell } from '@syncfusion/ej2-react-grids';
 import { Query } from '@syncfusion/ej2-data';
import { cascadeData  } from './datasource';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public countryParams : IEditCell = {
        params:   {
            allowFiltering: true,
            dataSource: this.country,
            fields: { text: "countryName", value: "countryName"},
            query: new Query(),
            actionComplete: () => false
            }
        };

    public country: { [key: string]: Object }[] = [
        { countryName: 'United States', countryId: '1' },
        { countryName: 'Australia', countryId: '2' },
        { countryName: 'India', countryId: '3' }
    ];

    render() {
        return <GridComponent dataSource={cascadeData} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={273}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150' editType= 'dropdownedit' edit={this.countryParams} textAlign="Right"></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Use Wizard like Dialog Editing

Wizard helps you create intuitive step-by-step forms to fill. You can achieve the wizard like editing by using the dialog template feature. It support your own editing template by defining [`editSettings.mode`](../api/grid/editSettings/#mode) as `Dialog` and [`editSetting.template`](../api/grid/editSettings/#template) as a REACT Component.

The following example demonstrate the wizard like editing in the grid with the obtrusive Validation.

{% tab template="grid/wizardediting", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';

class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog', template: this.dialogTemplate.bind(this) };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
    public grid: GridComponent;

    dialogTemplate(props: IOrderModel): any {
        let a = [props, this.grid]
      return (<DialogFormTemplate {...a} />);
    }

    actionComplete(args: DialogEditEventArgs): void {
        // Set initail Focus
        if (args.requestType === 'beginEdit') {
            (args.form.elements.namedItem('CustomerID') as HTMLInputElement).focus();
        } else if (args.requestType === 'add') {
            (args.form.elements.namedItem('OrderID')as HTMLInputElement).focus();
        }
    }

    render() {
        return <GridComponent ref={g=> this.grid = g} dataSource={data} actionComplete ={this.actionComplete.bind(this)} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true} validationRules= {{ required: true }}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120' validationRules= {{ required: true }}></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Using Tab Inside the Dialog Template

You can use [`tab`](../../tab/index.html) component inside dialog edit UI using dialog template feature. The dialog template feature can be enabled by defining  [`editSettings.mode`](../api/grid/editSettings/#mode) as `Dialog` and [`editSetting.template`](../api/grid/editSettings/#template) as a REACT Component.

The following example demonstrate the usage of tab control inside the dialog template.

{% tab template="grid/tabediting", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';

class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog', template: this.dialogTemplate.bind(this) };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
    public grid: GridComponent;

    dialogTemplate(props: IOrderModel): any {
        let a = [props, this.grid]
      return (<DialogFormTemplate {...a} />);
    }

    actionComplete(args: DialogEditEventArgs): void {
        // Set initail Focus
        if (args.requestType === 'beginEdit') {
            (args.form.elements.namedItem('CustomerID') as HTMLInputElement).focus();
        } else if (args.requestType === 'add') {
            (args.form.elements.namedItem('OrderID')as HTMLInputElement).focus();
        }
    }

    render() {
        return <GridComponent ref={g=> this.grid = g} dataSource={data} actionComplete={this.actionComplete.bind(this)} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true} validationRules= {{ required: true }}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120' validationRules= {{ required: true }}></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Disable editing for a particular row/cell

You can disable the editing for a particular row by using the [`actionBegin`](../api/grid/#actionbegin) event of Grid based on `requestType` as `beginEdit`.

In the below demo, the rows which are having the value for `ShipCountry` column as "France" is prevented from editing.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true };
    public toolbarOptions: ToolbarItems[] = ['Edit', 'Update', 'Cancel'];

    actionBegin(args: DialogEditEventArgs): void {
        if (args.requestType === 'beginEdit') {
            if (args.rowData.ShipCountry == "France") {
                args.cancel = true;
            }
        }
    }

    render() {
        return <GridComponent dataSource={data} actionBegin={this.actionBegin.bind(this)} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

For batch mode of editing, you can use [`cellEdit`](../api/grid/#celledit) event of Grid. In the below demo, the cells which are having the value as "France" is prevented from editing.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, mode: 'Batch' };
    public toolbarOptions: ToolbarItems[] = ['Edit', 'Update', 'Cancel'];

    cellEdit(args: DialogEditEventArgs): void {
        if (args.value == "France") {
            args.cancel = true;
        }
    }

    render() {
        return <GridComponent dataSource={data} cellEdit={this.cellEdit.bind(this)} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Perform Grid actions by keyboard shortcut keys

Using keyboard shortcuts, Grid performs navigation and actions.

In addition, You can also perform grid actions with custom keyboard shortcuts. This operation has to be achieved outside of the grid with the help of `keydown` event.

The following example demonstrates on `Adding` a new row when `Enter` key is pressed in the grid.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Normal' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
    private grid: GridComponent;

    load(args: DialogEditEventArgs): void {
        this.grid.element.addEventListener('keydown', this.keyDownHandler);
    }

    keyDownHandler(e: any): void {
        if(e.keyCode === 13) {
            let gridIns = this.ej2_instances[0];
            gridIns.addRecord();
        }
    }

    render() {
        return <GridComponent dataSource={data} load={this.load.bind(this)}
        editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265} ref={g => this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2' editType='numericedit'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Make a cell editable on a single click with batch editing

You can make a cell editable on a single click with `batch` mode of editing in Grid, by using the [`editCell`](../api/grid/column/#edit) method.

Bind the click event for the Grid and in the click event handler call the [`editCell`](../api/grid/column/#edit) method, based on the clicked target element.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
import { DialogFormTemplate, IOrderModel} from './template';
document.getElementById("grid").addEventListener("click", (e) => {
    if((event.target as any).classList.contains("e-rowcell")){
        let gridObj: any = (document.getElementsByClassName("e-grid")[0] as any).ej2_instances[0];
        let index: number = parseInt((event.target as any).getAttribute("Index"));
        let colindex:number = parseInt((event.target as any).getAttribute("aria-colindex"));
        let field:string = gridObj.getColumns()[colindex].field;
        gridObj.editModule.editCell(index, field);
    }
});

class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowAdding:true, allowDeleting:true, allowEditing: true, mode: 'Batch' };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

    render() {
        return <GridComponent id="Grid" dataSource={data} ref={grid => this.gridInstance = grid} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
        </GridComponent>
    }

};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

## Sort

### Perform single/multi sorting dynamically

You can perform single-column or multi-column sorting dynamically through an external button.

To perform single-column sorting, use the [`sortColumn`](../api/grid/sort/#sortcolumn) method of Grid.

```typescript
    public SingleSort():void {
      this.grid.sortColumn("OrderID","Descending")
    }
```

To perform multi-column sorting, you need to push the columns to be sorted into the [`sortSettings.columns`](../api/grid/sortSettingsModel/).

```typescript
    public MultiSort():void {
        this.grid.sortSettings.columns.push({ field: 'CustomerID',  direction: 'Ascending' },{ field: 'ShipName', direction: 'Descending' });
        this.grid.refresh();
    }
```

In the below demo, click on the corresponding button to perform single-column or multi-column sorting.

{% tab template="grid/change-headertext", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Sort } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public data: Object[] = data;
    private grid: GridComponent;
    public SingleSort():void {
      this.grid.sortColumn("OrderID","Descending")
    }
    public MultiSort():void {
        this.grid.sortSettings.columns.push({ field: 'CustomerID',  direction: 'Ascending' },{ field: 'ShipName', direction: 'Descending' });
        this.grid.refresh();
    }
    render() {
        return (<div>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.SingleSort.bind(this)}>Sort <b>OrderID</b> column</ButtonComponent>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.MultiSort.bind(this)}>Sort <b>CustomerID</b> and <b>ShipName</b> columns</ButtonComponent>
            <GridComponent dataSource={this.data} allowSorting={true} height={280} ref={g => this.grid = g}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[Sort]} />
            </GridComponent>
        </div>)
    }
}
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

### Dynamically clear sort for particular/entire sorted columns in Grid

You can clear the sorting for a particular column or the entire sorted columns in Grid dynamically through an external button.

To clear sort for a particular column, you need to splice the particular column from the [`sortSettings.columns`](../api/grid/sortSettings/#columns).

```typescript
    public SingleClearSort():void {
        let column: any = this.grid.sortSettings.columns;
        for(let i=0;i < column.length;i++) {
            if(column[i].field == "OrderID") {
                column.splice(i,1);
                this.grid.refresh();
            }
        }
    }
```

To clear sorting for all the sorted columns, use the [`clearSorting`](..(/api/grid/sort/#clearsorting) method of Grid.

```typescript
    public MultiClearSort():void {
        this.grid.clearSorting();
    }
```

In the below demo, click on the corresponding button to clear sort for particular or entire sorted columns in Grid.

{% tab template="grid/change-headertext", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import { data } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public data: Object[] = data;
    private grid: GridComponent;
    public SingleClearSort():void {
        let column: any = this.grid.sortSettings.columns;
        for(let i=0;i < column.length;i++) {
            if(column[i].field == "OrderID") {
                column.splice(i,1);
                this.grid.refresh();
            }
        }
    }
    public MultiClearSort():void {
        this.grid.clearSorting();
    }
    public sortingOptions: SortSettingsModel = { columns: [{ field: 'OrderID', direction: 'Ascending' }, { field: 'CustomerID', direction: 'Descending' }] };
    render() {
        return (<div>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.SingleClearSort.bind(this)}>Clear the sort for <b>OrderID</b> column</ButtonComponent>
            <ButtonComponent cssClass= 'e-flat' onClick= { this.MultiClearSort.bind(this)}>Clear sorting for entire sorted columns</ButtonComponent>
            <GridComponent dataSource={this.data} allowSorting={true} sortSettings={this.sortingOptions} height={280} ref={g => this.grid = g}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[Sort]} />
            </GridComponent>
        </div>)
    }
}
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

## Foreign Key

### Use Edit Template in Foreign Key Column

By default, foreign key column uses dropdown component for editing.
You can render other than the dropdown by using the [`column.edit`](../api/grid/column/#edit) property.
The following example demonstrates the way of using edit template in foreign column.

In the following example, The `Employee Name` is a foreign key column and while editing,
AutoComplete component is rendered instead of DropDownList.

{% tab template="grid/foreign-key", sourceFiles="app/**/index.tsx" %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GridComponent, ColumnsDirective, ColumnDirective, ForeignKey, Edit, Toolbar, Inject, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { createElement } from '@syncfusion/ej2-base';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { AutoComplete } from '@syncfusion/ej2-react-dropdowns';
import { data, employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public autoComplete: AutoComplete;
    public grid: GridComponent;
    public editOption: EditSettingsModel = {allowEditing: true};
    public toolbar: ToolbarItems = ['Edit', 'Update', 'Cancel'];
    public edit = {
                            create: () => { // to create input element
                                return createElement('input');
                            },
                            read: () => { // return edited value to update data source
                                let value: Object[] = new DataManager(employeeData).executeLocal(new Query().where('FirstName', 'equal', this.autoComplete.value));
                                return value.length && value[0]['EmployeeID']; // to convert foreign key value to local value.
                            },
                            destroy: () => { // to destroy the custom component.
                                this.autoComplete.destroy();
                            },
                            write: (args: { rowData: Object, column: Column, foreignKeyData: Object }) => { // to show the value for custom component
                                this.autoComplete = new AutoComplete({
                                    dataSource: employeeData,
                                    fields: { value: args.column.foreignKeyValue },
                                    value: args.foreignKeyData[0][args.column.foreignKeyValue]
                                });
                                this.autoComplete.appendTo(args.element);
                            }
                        };
    render() {
        return <GridComponent dataSource={data} height={280} editSettings= {this.editOption} toolbar={this.toolbar} ref={g => this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID' dataSource={employeeData}  headerText='Employee Name' width='150' edit={this.edit}></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2' editType='numericedit'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' ></ColumnDirective>
            </ColumnsDirective>
                <Inject services={[ForeignKey, Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Customize filter UI in foreign key column

You can create your own filtering UI by using [`column.filter`](../api/grid/column/#filter) property.
The following example demonstrates the way to create a custom filtering UI in the foreign column.

In the following example, The `Employee Name` is a foreign key column. DropDownList is rendered using Filter UI.

{% tab template="grid/foreign-key", sourceFiles="app/**/*.tsx" %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GridComponent, ColumnsDirective, ColumnDirective, ForeignKey, Filter, Inject, FilterSettingsModel } from '@syncfusion/ej2-react-grids';
import { data, fEmployeeData } from '../datasource.ts';
import { DataManager } from '@syncfusion/ej2-data';
import { createElement } from '@syncfusion/ej2-base';
import { DropDownList } from '@syncfusion/ej2-react-dropdowns';

class App extends React.Component<{}, {}>{
    public grid: GridComponent;
    public filterOption: FilterSettingsModel= {type: 'Menu'};
    public filter = {
            ui: {
                create: (args: { target: Element, column: Object }) => {
                    let flValInput: HTMLElement = createElement('input', { className: 'flm-input' });
                    args.target.appendChild(flValInput);
                    this.dropInstance = new DropDownList({
                        dataSource: new DataManager(fEmployeeData),
                        fields: { text: 'FirstName', value: 'EmployeeID' },
                        placeholder: 'Select a value',
                        popupHeight: '200px'
                    });
                    this.dropInstance.appendTo(flValInput);
                },
                write: (args: {
                    column: Object, target: Element, parent: any,
                    filteredValue: number | string
                }) => {
                    this.dropInstance.text = args.filteredValue || '';
                },
                read: (args: { target: Element, column: any, operator: string, fltrObj: Filter }) => {
                    args.fltrObj.filterByColumn(args.column.field, args.operator, this.dropInstance.text);
                }
            }
        };

    render() {
        return <GridComponent dataSource={data} height={315} allowFiltering={true}
        filterSettings={this.filterOption} ref={g => this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID' dataSource={fEmployeeData}  headerText='Employee Name' width='150' filter={this.filter}></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' ></ColumnDirective>
            </ColumnsDirective>
                <Inject services={[ForeignKey, Filter]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Use filter bar template in foreign key column

You can use the filter bar template in foreign key column by defining the
[`column.filterBarTemplate`](../api/grid/column/#filterbartemplate) property.
The following example demonstrates the way to use filter bar template in foreign column.

In the following example, The `Employee Name` is a foreign key column.
This column header shows the custom filter bar template and you can select filter value by using the `DropDown` options.

{% tab template="grid/foreign-key", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GridComponent, ColumnsDirective, ColumnDirective, ForeignKey, Filter, Inject } from '@syncfusion/ej2-react-grids';
import { data, fEmployeeData } from '../datasource.ts';
import { DataManager } from '@syncfusion/ej2-data';
import { createElement } from '@syncfusion/ej2-base';
import { DropDownList } from '@syncfusion/ej2-react-dropdowns';

class App extends React.Component<{}, {}>{
    public grid: GridComponent;
    public filterBarTemplate = {
                    create: (args: { element: Element, column: Column }) => {
                        return createElement('input', { className: 'flm-input' });
                    },
                    write: (args: { element: Element, column: Column }) => {
                        fEmployeeData.splice(0, 0, {'FirstName': 'All'}); // for clear filtering
                        let dropInstance: DropDownList = new DropDownList({
                            dataSource: new DataManager(fEmployeeData),
                            fields: { text: 'FirstName' },
                            placeholder: 'Select a value',
                            popupHeight: '200px',
                            index: 0,
                            change: (args) => {
                                if (args.value !== 'All') {
                                    this.grid.filterByColumn('EmployeeID', 'equal', args.value);
                                }
                                else {
                                    this.grid.removeFilteredColsByField('EmployeeID');
                                }
                            }
                        });
                        dropInstance.appendTo(args.element);
                    }
                };

    render() {
        return <GridComponent dataSource={data} height={280} allowFiltering={true} ref={g => this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID' dataSource={fEmployeeData}  headerText='Employee Name' width='150' filterBarTemplate={this.filterBarTemplate}></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' ></ColumnDirective>
            </ColumnsDirective>
                <Inject services={[ForeignKey, Filter]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Perform aggregation in Foreign Key Column

Default aggregations are not supported in a foreign key column.
You can achieve aggregation for the foreign key column by using the custom aggregates.
The following example demonstrates the way to achieve aggregation in foreign key column.

In the following example, The `Employee Name` is a foreign key column and the aggregation for the foreign column was calculated in customAggregateFn.

{% tab template="grid/foreign-key", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GridComponent, ColumnsDirective, ColumnDirective, ForeignKey, getForeignData, AggregateColumnModel, Aggregate, Inject } from '@syncfusion/ej2-react-grids';
import { data, employeeData } from '../datasource.ts';
import { getValue } from '@syncfusion/ej2-base';
class App extends React.Component<{}, {}>{
    public grid: GridComponent;
    public aggregate: AggregateColumnModel =  [
            {
                columns: [
                    {
                        type: 'Custom',
                        customAggregate: this.customAggregateFn,
                        field: 'EmployeeID',
                        footerTemplate: 'Count of Margaret: ${Custom}'
                    }
                ]
            }
        ];
    // Custom Aggregate function for foreign column
    public customAggregateFn(data: Object, column: AggregateColumnModel) {
        return data.result.filter((dObj: Object) => {
            return getValue('FirstName' , getForeignData(this.getColumnByField(column.field), dObj)[0]) === 'Margaret';
        }).length;
    };
    render() {
        return <GridComponent dataSource={data} height={280} aggregates={this.aggregate} ref={g => this.grid = g}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID' dataSource={employeeData}  headerText='Employee Name' width='150'></ColumnDirective>
                    <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'></ColumnDirective>
                    <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' ></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[ForeignKey, Aggregate]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

### Bind foreign key dataSource on dropdown edit

When editing, you can bind foreign key datasource to a dropdown list by using [`column.dataSource`](../api/grid/column/#datasource) property.

{% tab template="grid/foreign-key", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GridComponent, ColumnsDirective, ColumnDirective, ForeignKey, Inject, Edit, Toolbar,
EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import { data, employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

    render() {
        return <GridComponent dataSource={data} editSettings={this.editOptions} toolbar={this.toolbarOptions} height={315}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"></ColumnDirective>
                <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID' dataSource={employeeData}  headerText='Employee Name' width='150'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' ></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[ForeignKey, Edit, Toolbar]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

> * By default, the foreign key column's `editType` will be set as `dropdownedit`.

## Exporting

### Exporting Filtered Data Only

You can export the filtered data by defining the resulted data in `exportProperties.dataSource` before export.

In the below Pdf exporting demo, We have gotten the filtered data by applying filter query to the grid data and then defines the resulted data in `exportProperties.dataSource` and pass it to `pdfExport` method.

 {% tab template="grid/export-filtered-data", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GridComponent, ColumnsDirective, ColumnDirective, Inject, Page, PageSettingsModel, Filter,
Toolbar, ToolbarItems, PdfExport } from '@syncfusion/ej2-react-grids';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { data } from '../datasource.ts';
import { ClickEventArgs } from '@syncfusion/ej2-react-navigations';
class App extends React.Component<{}, {}>{
    public grid: GridComponent;
    public pageOptions: PageSettingsModel = {pageSize:5, pageCount:5};
    public toolbar: ToolbarItems[] = ['PdfExport'];
    toolbarClick = (args: ClickEventArgs) => {
      if (args.item.id === 'grid_pdfexport') {
        let pdfdata: Object[];
        let query = this.grid.renderModule.data.generateQuery(); // get grid corresponding query
        for(var i=0; i<query.queries.length; i++ ){
            if(query.queries[i].fn=='onPage'){
             query.queries.splice(i,1);     // remove page query to get all records
             break;
            }
        }
        let fdata: Object[] = new DataManager({ json: data}).executeQuery(query).then((e: any) => {
          pdfdata = e.result;   // get all filtered records
          let exportProperties = {
            dataSource: pdfdata,
          };
          this.grid.pdfExport(exportProperties);
        }).catch((e) => true);
      }
    }
    render() {
        return <GridComponent id='grid' dataSource={data} allowPaging={true}
        allowFiltering={true} allowPdfExport={true} toolbar={this.toolbar}
        pageSettings={this.pageOptions} toolbarClick={this.toolbarClick.bind(this)}
        ref={g => this.grid = g}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Page, Filter,Toolbar, PdfExport]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

## Pager

### Customize Pager DropDown

To customize default values of pager dropdown, you need to define `pageSizes` as array of strings.

{% tab template="grid/pagerdropdown", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = {pageSizes: ["5", "10", "All"]};
    public gridObj: GridComponent;
    render() {
        return <GridComponent dataSource={data} allowPaging={true} ref={grid => this.gridObj = grid} pageSettings={this.pageOptions} height={273}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}></ColumnDirective>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'></ColumnDirective>
                <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"></ColumnDirective>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Page]} />
        </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}

## Hide the expand/collapse icon in parent row with no record in child grid

By default, the expand/collapse icon will be visible even if the child grid is empty.

You can use [`rowDataBound`](../api/grid/#rowdatabound) event to hide the icon when there is no record in child grid.

To hide the expand/collapse icon in parent row with no record in child grid, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .e-row[aria-selected="true"] .e-customizedExpandcell {
        background-color: #e0e0e0;
    }

    .e-grid.e-gridhover tr[role='row']:hover {
        background-color: #eee;
    }

```

**Step 2**:

Add the CSS class to the Grid in the [`rowDataBound`](../api/grid/#rowdatabound) event handler of Grid.

```typescript
    public rowDataBound(args:any){
        let filter:string = args.data.EmployeeID;
        let childrecord: any = new DataManager(this.Grid.childGrid.dataSource).executeLocal(new Query().where("EmployeeID", "equal", parseInt(filter), true));
        if(childrecord.length == 0) {
            //here hide which parent row has no child records
            args.row.querySelector('td').innerHTML=" ";
            args.row.querySelector('td').className = "e-customizedExpandcell";
        }
    }

```

In the below demo, the expand/collapse icon in the row with `EmployeeID` as `1` is hidden as it does not have record in child Grid.

{% tab template="grid/customizedialog", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DataManager, Query } from '@syncfusion/ej2-data';
import { GridComponent, Inject, DetailRow, ColumnsDirective, ColumnDirective, GridModel } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    private Grid: GridComponent;
    public dataManger: Object = [{Order:100, ShipName:'Berlin', EmployeeID:2},
                                 {Order:101, ShipName:'Capte', EmployeeID:3},
                                 {Order:102, ShipName:'Marlon', EmployeeID:4},
                                 {Order:103, ShipName:'Black pearl', EmployeeID:5},
                                 {Order:104, ShipName:'Pearl', EmployeeID:6},
                                 {Order:105, ShipName:'Noth bay', EmployeeID:7},
                                 {Order:106, ShipName:'baratna', EmployeeID:8},
                                 {Order:107, ShipName:'Charge', EmployeeID:9}];
    public childGrid : GridModel = {
        dataSource: this.dataManger,
        queryString: 'EmployeeID',
        columns: [
            { field: 'Order', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'EmployeeID', headerText: 'EmployeeID', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
    };
    rowDataBound(args:any): void{
        let filter:string = args.data.EmployeeID;
        let childrecord: any = new DataManager(this.Grid.childGrid.dataSource).executeLocal(new Query().where("EmployeeID", "equal", parseInt(filter), true));
        if(childrecord.length == 0) {
            //here hide which parent row has no child records
            args.row.querySelector('td').innerHTML=" ";
            args.row.querySelector('td').className = "e-customizedExpandcell";
        }
    }

    render() {
        return <GridComponent dataSource={data} childGrid={this.childGrid} rowDataBound={this.rowDataBound.bind(this)} ref={(scope) => { this.Grid = scope; }}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' width='100' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' width='100'></ColumnDirective>
                    <ColumnDirective field='EmployeeID' width='100' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='ShipCountry' width='100'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[DetailRow]}/>
            </GridComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('grid'));
```

{% endtab %}