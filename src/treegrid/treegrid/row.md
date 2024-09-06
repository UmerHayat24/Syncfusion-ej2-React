---
title: "Row"
component: "TreeGrid"
description: "Documentation for row customizations in TreeGrid."
---

# Row

The row represents record details fetched from data source.

To get start quickly with features in Row, you can check on this video:
`youtube:mHo_WLeNtWI`

## Customize Rows

You can customize the appearance of a row by using the [`rowDataBound`](../api/treegrid/#rowdatabound) event.
The [`rowDataBound`](../api/treegrid/#rowdatabound) event triggers for every row. In the event handler, you can get the
[`RowDataBoundEventArgs`](../api/grid/rowDataBoundEventArgs/) that contains details of the row.

{% tab template="treegrid/rows", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject, RowDataBoundEventArgs } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public rowDataBound(args: RowDataBoundEventArgs) {
        if (getObject('duration', args.data) === 0 ) {
            (args.row as HTMLTableRowElement).style.background= '#336c12';
        } else if (getObject('duration', args.data) < 3) {
            (args.row as HTMLTableRowElement).style.background= '#7b2b1d';
        }
    }

    public render() {
        this.rowDataBound = this.rowDataBound.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='275' rowDataBound={this.rowDataBound} enableHover='false'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Styling alternate row

You can change the treegrid's alternative rows' background color by overriding the *.e-altrow* class.

```css
.e-treegrid .e-altrow {
    background-color: #fafafa;
}
```

Please refer the following example.

{% tab template="treegrid/alt-row", sourceFiles="app/App.tsx,custom.css", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import './custom.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='275' enableHover='false'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Row height

You can customize the row height of treegrid rows through the [`rowHeight`](../api/treegrid/#rowheight) property. The **rowHeight** property is used to change the row height of entire treegrid rows.

In the below example, the **rowHeight** is set as *60px*.

{% tab template="treegrid/rows", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='275' rowHeight='60'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Customize row height for particular row

TreeGrid row height for particular row can be customized using the [`rowDataBound`](../api/treegrid/#rowdatabound)
event by setting the **rowHeight** in arguments for each row based on the requirement.

In the below example, the row height for the row with Task ID as *3* is set as *90px* using the **rowDataBound** event.

{% tab template="treegrid/rows", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject, RowDataBoundEventArgs } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public rowDataBound(args: RowDataBoundEventArgs) {
        if(getObject('taskID', args.data) === 3){
            args.rowHeight = 90;
        }
    }

    public render() {
        this.rowDataBound = this.rowDataBound.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         height='275' rowDataBound={this.rowDataBound}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Row template

The [`rowTemplate`](../api/treegrid/#rowtemplate) has an option to customise the look and behavior of the treegrid rows. The [`rowTemplate`](../api/treegrid/#rowtemplate) property accepts either the template string or HTML element ID.

{% tab template="treegrid/rowtemplate", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { textdata } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegridTemplate(props): any {
        var src = './' + props.FullName + '.png';
        return (<tr>
            <td className="border"  style={{paddingLeft:'18px'}}>
                <div>{props.EmpID}</div>
            </td>
            <td className="border"  style={{padding: '10px 0px 0px 20px'}}>
                <div style={{fontSize:'14px'}}>
                  {props.Name}
                    <p style={{fontSize:'9px'}}>{props.Designation}</p>
                </div>
            </td>
            <td className="border">
                <div>
                    <div style={{position:'relative' , display:'inline-block'}}>
                        <img src ={src} />
                    </div>
                    <div style={{display:'inline-block'}}>
                        <div style={{padding:'5px'}}>{props.Address}</div>
                        <div style={{padding:'5px'}}>{props.Country}</div>
                        <div style={{padding:'5px' ,fontSize: '12px'}}>{props.Contact}</div>
                    </div>
                </div>
            </td>
    </tr>);
    }
    public template: any = this.treegridTemplate;
    public render() {
        return <TreeGridComponent dataSource={textdata} childMapping = 'Children' rowTemplate={this.template.bind(this)} treeColumnIndex={0} rowHeight = '83' height='291'>
                <ColumnsDirective>
                <ColumnDirective headerText = 'Employee ID' width = '180' field = 'EmpID'></ColumnDirective>
                <ColumnDirective headerText = 'Employee Name' width = '150' field = 'Name'></ColumnDirective>
                <ColumnDirective headerText = 'Employee Details' width = '350' field = 'Address'></ColumnDirective>
                </ColumnsDirective>
                </TreeGridComponent>
    }
}
```

{% endtab %}

The [`rowTemplate`](../api/treegrid/#rowtemplate) property accepts only the TR element.

### Row template with formatting

If the [`rowTemplate`](../api/treegrid/#rowtemplate) is used, the value cannot be  formatted  inside the template using the [`columns.format`](../api/treegrid/column/#format) property. In that case, a function should be defined globally to format the value and invoke it inside the template.

{% tab template="treegrid/rowtemplateformat", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { textdata } from './datasource';
import { Internationalization } from '@syncfusion/ej2-base';

let instance: Internationalization = new Internationalization();

interface DateFormat extends Window {
    format?: Function;
}

export default class App extends React.Component<{}, {}>{
    public format = (value: Date) => {
        return instance.formatDate(value, { skeleton: 'yMd', type: 'date' });
    }
    public treegridTemplate(props): any {
        var src = './' + props.FullName + '.png';
        return (<tr>
            <td className="border"  style={{paddingLeft:'18px'}}>
                <div>{props.EmpID}</div>
            </td>
            <td className="border">
                <div>
                    <div style={{position:'relative' , display:'inline-block'}}>
                        <img src ={src} />
                    </div>
                    <div style={{display:'inline-block'}}>
                        <div style={{padding:'5px'}}>{props.Address}</div>
                        <div style={{padding:'5px'}}>{props.Country}</div>
                        <div style={{padding:'5px' ,fontSize: '12px'}}>{props.Contact}</div>
                    </div>
                </div>
            </td>
            <td className="border" style={{paddingLeft:'20px'}}>
                <div>{this.format(props.DOB)}</div>
            </td>
    </tr>);
    }
    public template: any = this.treegridTemplate;
    public render() {
        return <TreeGridComponent dataSource={textdata} childMapping = 'Children' rowTemplate={this.template.bind(this)} treeColumnIndex={0} rowHeight = '83' height='291'>
                <ColumnsDirective>
                <ColumnDirective headerText = 'Employee ID' width = '180' field = 'EmpID'></ColumnDirective>
                <ColumnDirective headerText = 'Employee Details' width = '350' field = 'Address'></ColumnDirective>
                <ColumnDirective headerText = 'DOB' width = '150' field = 'DOB'></ColumnDirective>
                </ColumnsDirective>
                </TreeGridComponent>
    }
}
```

{% endtab %}

### Limitations

Row template feature is not compatible with all the features which are available in treegrid and it has limited features support. Here we have listed out the features which are compatible with row template feature.

* Filtering
* Paging
* Sorting
* Scrolling
* Searching
* Rtl
* Context Menu
* State Persistence

## Detail template

The detail template provides additional information about a particular row. By expanding the parent row the child rows are expanded along with their detail template. The [`detailTemplate`](../api/treegrid/#detailtemplate) property accepts either the template string or HTML element ID.

To use detail template, inject the DetailRow module in the TreeGrid.

{% tab template="treegrid/detailtemplate", sourceFiles="app/App.tsx, index.html", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent, DetailRow, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { textdata } from './datasource';
import { Internationalization } from '@syncfusion/ej2-base';

let instance: Internationalization = new Internationalization();

interface DateFormat extends Window {
    format?: Function;
}

export default class App extends React.Component<{}, {}>{
    public format = (value: Date) => {
        return instance.formatDate(value, { skeleton: 'yMd', type: 'date' });
    }

 public detailtemplate(props): any {
        var imag = './' + props.FullName + '.png';
        return (
            <div>
                <div style={{ position: 'relative', display: 'inline-block', float: 'left', padding: '5px 4px 2px 27px' }} >
                    <img src={imag} />
                </div>
                <div style={{ paddingLeft: '10px', display: 'inline-block', width: '66%', fontSize: '13px', fontFamily: 'Segoe UI' }}>
                    <div className="e-description" style={{ marginTop: '5px' }}>
                        <b>{props.Name}</b> was born on {this.format(props.DOB)}. Now lives at {props.Address}, {props.Country}. {props.Name} holds a position of <b>{props.Designation}</b> in our WA department, (Seattle USA).</div>
                    <div className="e-description" style={{ marginTop: '5px' }}>
                        <b style={{ marginRight: '10px' }}>Contact:</b>{props.Contact}
                    </div>
                </div>
            </div>
        );
    }
    public template: any = this.detailtemplate;
    render() {
        return (
            <div className='control-pane'>
                <div className='control-section'>
                    <TreeGridComponent dataSource={textdata} childMapping='Children' detailTemplate={this.template.bind(this)} treeColumnIndex={0}>
                        <ColumnsDirective>
                            <ColumnDirective headerText='Full Name' width='170' field='Name'></ColumnDirective>
                            <ColumnDirective field='Designation' headerText='Designation' width='180'></ColumnDirective>
                            <ColumnDirective field='EmpID' headerText='EmployeeID' width='110'></ColumnDirective>
                            <ColumnDirective field='Country' headerText='Country' width='90'></ColumnDirective>
                        </ColumnsDirective>
                        <Inject services={[DetailRow]} />
                    </TreeGridComponent>
                </div>
            </div>
        )
    }
}
```

{% endtab %}

## Drag and drop

The TreeGrid rows can be reordered, dropped to another TreeGrid or custom control by enabling the [`allowRowDragAndDrop`](../api/treegrid/#allowrowdraganddrop) to true.

To use row drag and drop, inject the `RowDD` module in the TreeGrid.

### Drag and drop within TreeGrid

The TreeGrid row drag and drop allows you to drag and drop TreeGrid rows on the same TreeGrid using drag icon. To enable row drag and drop, set the [`allowRowDragAndDrop`](../api/treegrid/#allowrowdraganddrop) to true. It provides the way to drop the row above, below or child to the target row with respective to the target row position.

{% tab template="treegrid/row", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, RowDD, RowDropSettingsModel, SelectionSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { sampleData } from './datasource';

class App extends React.Component<{}, {}>{

    public selectionSettings: SelectionSettingsModel = { type: 'Multiple' };

    render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270' selectionSettings={this.selectionSettings} >
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'></ColumnDirective>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'></ColumnDirective>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[RowDD]}/>
        </TreeGridComponent>
    }
}
ReactDOM.render(<App />, document.getElementById('treegrid'));
```

{% endtab %}

> * Selection feature must be enabled for row drag and drop.
> * Multiple rows can be selected by clicking and dragging inside the treegrid.
> * For multiple row selection, the [`type`](../api/treegrid/selectionSettings/#type) property must be set to `multiple`.

### Drag and drop to another TreeGrid

To drag and drop between two TreeGrid, enable the [`allowRowDragAndDrop`](../api/treegrid/#allowrowdraganddrop) property and specify the target TreeGrid ID in [`targetID`](../api/treegrid/rowDropSettings/#targetid) property of rowDropSettings.

{% tab template="treegrid/row", sourceFiles="app/**/index.tsx, index.html" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TreeGridComponent, RowDD, ColumnsDirective, ColumnDirective, RowDropSettingsModel, SelectionSettingsModel, Inject } from '@syncfusion/ej2-react-treegrid';
import { sampleData } from './datasource';

class Source extends React.Component<{}, {}>{
    public data: Object[] = sampleData;
    public rowDropSettings: RowDropSettingsModel = { targetID: 'DestGrid' };
    public selectionSettings: SelectionSettingsModel = { type: 'Multiple' };
    public style = { marginBottom: '20px' };
    render() {
        return <TreeGridComponent id='TreeGrid' dataSource={sampleData} treeColumnIndex={1} allowRowDragAndDrop={true}
        rowDropSettings={this.rowDropSettings} selectionSettings={this.selectionSettings}
         childMapping='subtasks' height='275'}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'></ColumnDirective>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'></ColumnDirective>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[RowDD]}/>
        </TreeGridComponent>
    }
}

class Target extends React.Component<{}, {}>{
    public data: Object[] = [];
    public rowDropSettings: RowDropSettingsModel = { targetID: 'TreeGrid' };
    public selectionSettings: SelectionSettingsModel = { type: 'Multiple' };
    render() {
        return <TreeGridComponent treeColumnIndex={1} id='DestGrid' allowRowDragAndDrop={true}
        rowDropSettings={this.rowDropSettings} selectionSettings={this.selectionSettings}
         childMapping='subtasks' height='275'}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'></ColumnDirective>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'></ColumnDirective>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[RowDD]}/>
        </TreeGridComponent>
    }
}


function App(){
    return <div>
            <Source></Source>
            <Target></Target>
           </div>
}

ReactDOM.render(<App />, document.getElementById('treegrid'));

```

{% endtab %}

### Drag and drop events

The following events are triggered while drag and drop the treegrid rows.

[`rowDragStartHelper`](../api/treegrid/#rowdragstarthelper) - Triggers when click the drag icon or treegrid row and this event is used to customize the drag element based on user criteria.<br/>
[`rowDragStart`](../api/treegrid/#rowdragstart) -Triggers when starts to drag the treegrid row. <br/>
[`rowDrag`](../api/treegrid/#rowdrag) - Triggers while dragging the treegrid row. <br/>
[`rowDrop`](../api/treegrid/#rowdrop) - Triggers when a drag element is dropped on the target element. <br/>
