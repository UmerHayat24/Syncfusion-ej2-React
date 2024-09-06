---
title: "Row"
component: "Grid"
description: "Documentation for row templates (custom row content), detail templates, and DataGrid row styles."
---

# Row

It represents the record details that are fetched from the [`dataSource`](../api/grid/#datasource).

## Drag and Drop

The Grid Row drag and drop allows you to drag grid rows and drop to another Grid or custom component.
To enable Row drag and drop in the Grid, set the [`allowRowDragAndDrop`](../api/grid/#allowrowdraganddrop) to true.
The target component on which the Grid rows to be dropped can be set by using
[`targetID`](../api/grid/rowDropSettings/#targetid).

To use Row Drag and Drop, you need to inject **RowDD** module in Grid.

{% tab template="grid/row-drag", sourceFiles="app/App.tsx,app/DestGrid.tsx,app/SourceGrid.tsx" %}

```typescript
import * as React from 'react';
import { Target } from './DestGrid';
import { Source } from './SourceGrid';

export default class App extends React.Component<{}, {}>{
  public render () {
    return (<div>
          <Source/>
          <Target/>
         </div>)
  }
}
```

{% endtab %}

> * **Selection** feature must be enabled for row drag and drop.
> * Multiple rows can be selected by clicking and dragging inside the Grid.
For multiple row selection, the [`selectionSettings.type`](../api/grid/selectionSettings/#type) property must be set to **Multiple**.

## Row spanning

The grid has option to span row cells. To achieve this, You need to define the [`rowSpan`](../api/grid/queryCellInfoEventArgs/#rowspan) attribute to span cells in the [`QueryCellInfo`](../api/grid/#querycellinfo) event.

In the following demo, **Davolio** cell is spanned to two rows in the **EmployeeName** column.

Also Grid supports the spanning of rows and columns for same cells. **Lunch Break** cell is spanned to all the rows and three columns in the **1:00** column.

{% tab template="grid/spanning", sourceFiles="app/App.tsx,app/datasource.tsx,app/ColumnSpanDataType.tsx" %}

```typescript
import { Column, ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { IColumnSpanDataType } from './colspanDataType';
import { columnSpanData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public queryCellInfoEvent = (args: QueryCellInfoEventArgs) => {
    const col: Column = args.column as Column;
    const data: IColumnSpanDataType = args.data as IColumnSpanDataType;
    switch (data.EmployeeID) {
        case 10001:
            if (col.field === '9:00' || col.field === '2:30' || col.field === '4:30') {
                args.colSpan = 2;
            } else if (col.field === '11:00') {
                args.colSpan = 3;
            } else if (col.field === 'EmployeeName') {
              args.rowSpan = 2;
            } else if (col.field === '1:00') {
                args.colSpan = 3;
                args.rowSpan = (this.grid && this.grid.currentViewData.length) || 0;
            }
            break;
        case 10002:
            if (col.field === '9:30' || col.field === '2:30' ||
                col.field === '4:30') {
                args.colSpan = 3;
            } else if (col.field === '11:00') {
                args.colSpan = 4;
            }
            break;
        case 10003:
            if (col.field === '9:00' || col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '10:30' || col.field === '3:30' ||
                col.field === '4:30' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 10004:
            if (col.field === '9:00') {
                args.colSpan = 3;
            } else if (col.field === '11:00') {
                args.colSpan = 4;
            } else if (col.field === '4:00' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 10005:
            if (col.field === '9:00') {
                args.colSpan = 4;
            } else if (col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '3:30' || col.field === '4:30' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 10006:
            if (col.field === '9:00' || col.field === '4:30' ||
                col.field === '2:30' || col.field === '3:30') {
                args.colSpan = 2;
            } else if (col.field === '10:00' || col.field === '11:30') {
                args.colSpan = 3;
            }
            break;
        case 10007:
            if (col.field === '9:00' || col.field === '3:00' || col.field === '10:30') {
                args.colSpan = 2;
            } else if (col.field === '11:30' || col.field === '4:00') {
                args.colSpan = 3;
            }
            break;
        case 10008:
            if (col.field === '9:00' || col.field === '10:30' || col.field === '2:30') {
                args.colSpan = 3;
            } else if (col.field === '4:00') {
                args.colSpan = 2;
            }
            break;
        case 10009:
            if (col.field === '9:00' || col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '4:30' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 100010:
            if (col.field === '9:00' || col.field === '2:30' ||
                col.field === '4:00' || col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '10:30') {
                args.colSpan = 2;
            }
            break;
    }
};
public render() {
    this.queryCellInfoEvent = this.queryCellInfoEvent.bind(this);
    return (
        <div className='control-pane'>
            <div className='control-section'>
                <GridComponent dataSource={columnSpanData} ref={g => this.grid = g} queryCellInfo={this.queryCellInfoEvent} allowTextWrap={true} height='auto' width='auto' gridLines='Both' >
                    <ColumnsDirective>
                        <ColumnDirective field='EmployeeID' headerText='Employee ID' width='150' textAlign='Right'/>
                        <ColumnDirective field='EmployeeName' headerText='Employee Name' width='200' />
                        <ColumnDirective field='9:00' headerText='9:00 AM' width='120'/>
                        <ColumnDirective field='9:30' headerText='9:30 AM' width='120'/>
                        <ColumnDirective field='10:00' headerText='10:00 AM' width='120'/>
                        <ColumnDirective field='10:30' headerText='10:30 AM' width='120'/>
                        <ColumnDirective field='11:00' headerText='11:00 AM' width='120'/>
                        <ColumnDirective field='11:30' headerText='11:30 AM' width='120'/>
                        <ColumnDirective field='12:00' headerText='12:00 PM' width='120'/>
                        <ColumnDirective field='12:30' headerText='12:30 PM' width='120'/>
                        <ColumnDirective field='1:00' headerText='1:00 PM' textAlign='Center' width='120'/>
                        <ColumnDirective field='1:30' headerText='1:30 PM' width='120'/>
                        <ColumnDirective field='2:00' headerText='2:00 PM' width='120'/>
                        <ColumnDirective field='2:30' headerText='2:30 PM' width='120'/>
                        <ColumnDirective field='3:00' headerText='3:00 PM' width='120'/>
                        <ColumnDirective field='3:30' headerText='3:30 PM' width='120'/>
                        <ColumnDirective field='4:00' headerText='4:00 PM' width='120'/>
                        <ColumnDirective field='4:30' headerText='4:30 PM' width='120'/>
                        <ColumnDirective field='5:00' headerText='5:00 PM' width='120'/>
                    </ColumnsDirective>
                </GridComponent>
            </div>
        </div>
    )
}
};
```

{% endtab %}

> To disable the spanning for particular Grid page, use [`requestType`](../api/grid/queryCellInfoEventArgs/#requesttype) from [`QueryCellInfo`](../api/grid/#querycellinfo) event argument.

## Customize Rows

You can customize the appearance of the Row by using the [`rowDataBound`](../api/grid/#rowdatabound) event.
The [`rowDataBound`](../api/grid/#rowdatabound) event triggers for every row. In that event handler,
you can get [`RowDataBoundEventArgs`](../api/grid/rowDataBoundEventArgs/) which contain details of the row.

{% tab template="grid/rows", sourceFiles="app/App.tsx,custom.css,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, RowDataBoundEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public rowDataBound(args: RowDataBoundEventArgs) {
      if (args.row) {
        if (getValue('Freight', args.data) < 30){
          args.row.classList.add('below-30');
        } else if(getValue('Freight', args.data) < 80 ) {
            args.row.classList.add('below-80');
        } else {
            args.row.classList.add('above-80');
        }
      }
  }
  public render() {
      return (<div>
      <GridComponent dataSource={data} height={315} enableHover={false} allowSelection={false}
          rowDataBound={this.rowDataBound}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
              <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right"/>
              <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
          </ColumnsDirective>
      </GridComponent>
      </div>)
  }
}
```

{% endtab %}

## Styling alternate row

Grid alternative rows has **e-altrow** class. So, you can change alternative background color by overriding **e-altrow** class.

```css
.e-grid .e-altrow {
    background-color: #fafafa;
}
```

Please refer the following example.

{% tab template="grid/rows-alt", sourceFiles="app/App.tsx,custom.css,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public pageSettings: PageSettingsModel = { pageSize: 7 };
  public render() {
    return <GridComponent dataSource={data} allowPaging={true} pageSettings={this.pageSettings}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Page]} />
    </GridComponent>
  }
}
```

{% endtab %}

## See Also

* [Row drag and drop within the Grid using remote data in React Grid](https://www.syncfusion.com/forums/147119/row-drag-and-drop-within-the-grid-using-remote-data-in-react-grid)