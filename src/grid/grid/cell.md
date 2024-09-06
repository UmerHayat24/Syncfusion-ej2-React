---
title: "Cell"
component: "Grid"
description: "Learn how to customize the Essential JS 2 DataGrid cells with styling, text wrapping, adding custom attributes and tooltips."
---

# Cell

## Displaying HTML Content

The HTML tags can be displayed in the Grid header and content by enabling the
 [`disableHtmlEncode`](../api/grid/column/#disablehtmlencode) property.

{% tab template="grid/display-html", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
      return (<div>
      <GridComponent dataSource={data} height={315}>
          <ColumnsDirective>
              <ColumnDirective field="OrderID" headerText="<span> Order ID </span>" disableHtmlEncode={true} width="140" textAlign="Right"/>
              <ColumnDirective field="CustomerID" headerText="<span> Customer ID </span>" disableHtmlEncode={false} width="100"/>
              <ColumnDirective field="EmployeeID" headerText="Employee ID" width="100" textAlign="Right"/>
              <ColumnDirective field="Freight" headerText="Freight" width="80" format="C2" textAlign="Right"/>
              <ColumnDirective field="ShipCountry" headerText="Ship Country" width="100"/>
          </ColumnsDirective>
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## Customize Cell Styles

The appearance of cells can be customized by using the [`queryCellInfo`](../api/grid/#querycellinfo) event.
The [`queryCellInfo`](../api/grid/#querycellinfo) event triggers for every cell.
In that event handler, you can get
[`QueryCellInfoEventArgs`](../api/grid/queryCellInfoEventArgs/) that contains the details of the cell.

{% tab template="grid/rows", sourceFiles="app/App.tsx,custom.css,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { Column, ColumnDirective, ColumnsDirective, GridComponent, QueryCellInfoEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public customizeCell(args: QueryCellInfoEventArgs) {
      if((args.column as Column).field === "Freight"
        && args.data && args.cell) {
          if (getValue('Freight', args.data) < 30){
              args.cell.classList.add('below-30');
          } else if(getValue('Freight', args.data) < 80 ) {
              args.cell.classList.add('below-80');
          } else {
              args.cell.classList.add('above-80');
          }
      }
  }
  public render() {
      return (<div>
      <GridComponent dataSource={data} height={315} enableHover={false} allowSelection={false}
          queryCellInfo={this.customizeCell}>
          <ColumnsDirective>
              <ColumnDirective field="OrderID" headerText="Order ID" width="100" textAlign="Right"/>
              <ColumnDirective field="CustomerID" headerText="Customer ID" width="100"/>
              <ColumnDirective field="EmployeeID" headerText="Employee ID" width="100" textAlign="Right"/>
              <ColumnDirective field="Freight" headerText="Freight" width="80" textAlign="Right" format="C2" />
              <ColumnDirective field="ShipCountry" headerText="Ship Country" width="100"/>
          </ColumnsDirective>
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## Auto Wrap

The auto wrap allows the cell content of the grid to wrap to the next line when it exceeds the boundary of the cell width. The Cell Content wrapping works based on the position of white space between words.
To enable auto wrap, set the [`allowTextWrap`](../api/grid/#allowtextwrap) property to **true**.
You can configure the auto wrap mode by setting the [`textWrapSettings.wrapMode`](../api/grid/textWrapSettings/#wrapmode) property.

There are three types of [`wrapMode`](../api/grid/textWrapSettings/#wrapmode). They are

* **Both** - It is the default value. Auto wrap will be enabled for both content and Header.
* **Header** - Auto wrap will be enabled only for header.
* **Content** - Auto wrap will be enabled only for content.

> When a column width is not specified, then auto wrap of columns will be adjusted with respect to the Grid's width.

In the below example, the [`textWrapSettings.wrapMode`](../api/grid/textWrapSettings/#wrapmode) is set as **Content**.

{% tab template="grid/autowrap", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, TextWrapSettingsModel } from '@syncfusion/ej2-react-grids';
import { Inject, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { inventoryData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public settings: TextWrapSettingsModel  = { wrapMode: 'Content' };
  public render() {
      return (<div>
      <GridComponent dataSource={inventoryData} allowPaging={true} allowTextWrap={true}
          textWrapSettings={this.settings} height='400'>
          <ColumnsDirective>
              <ColumnDirective field='Inventor' headerText='Inventor' width='180' textAlign='Right'/>
              <ColumnDirective field='NumberofPatentFamilies' headerText='Number of Patent Families' width='180' textAlign='Right'/>
              <ColumnDirective field='Country' headerText='Country' width="140" />
              <ColumnDirective field='Active' headerText='Active' width='120' />
              <ColumnDirective field='Mainfieldsofinvention' headerText='Main Fields of Invention' width='200'/>
          </ColumnsDirective>
          <Inject services={[Page]} />
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## Custom Attributes

You can customize the grid cells by adding a CSS class to the [`customAttribute`](../api/grid/column#customattributes) property of the column.

```CSS
.e-attr {
    background: #d7f0f4;
}
```

```typescript
<ColumnDirective
    field="ShipCity" headerText="Ship City" :customAttributes={{class: 'e-attr'}} width="80">
</ColumnDirective>
```

In the below example, we have customized the cells of **OrderID** and **ShipCity** columns.

{% tab template="grid/customize-cell", sourceFiles="app/App.tsx,custom.css,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return (<div>
    <GridComponent dataSource={data} height={315}>
        <ColumnsDirective>
            <ColumnDirective field="OrderID" headerText="Order ID" customAttributes={{class: 'e-attr'}} width="100" textAlign="Right"/>
            <ColumnDirective field="CustomerID" headerText="Customer ID" width="100"/>
            <ColumnDirective field="ShipCity" headerText="Ship City" customAttributes={{class: 'e-attr'}} width="100"/>
            <ColumnDirective field="ShipCountry" headerText="Ship Country" width="100"/>
        </ColumnsDirective>
    </GridComponent>
    </div>)
   }
};
```

{% endtab %}

## Grid Lines

The [`gridLines`](../api/grid/#gridlines) have option to display cell border and it can be defined by the
[`gridLines`](../api/grid/#gridlines) property.

The available modes of grid lines are:

| Modes | Actions |
|-------|---------|
| Both | Displays both the horizontal and vertical grid lines.|
| None | No grid lines are displayed.|
| Horizontal | Displays the horizontal grid lines only.|
| Vertical | Displays the vertical grid lines only.|
| Default | Displays grid lines based on the theme.|

{% tab template="grid/autowrap", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { inventoryData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return (<div>
    <GridComponent dataSource={inventoryData} gridLines='Both' height={315}>
        <ColumnsDirective>
            <ColumnDirective field='Inventor' headerText='Inventor' width='180' textAlign='Right'/>
            <ColumnDirective field='NumberofPatentFamilies' headerText='Number of Patent Families' width='180' textAlign='Right'/>
            <ColumnDirective field='Country' headerText='Country' width="140" />
            <ColumnDirective field='Active' headerText='Active' width='120' />
            <ColumnDirective field='Mainfieldsofinvention' headerText='Main Fields of Invention' width='200'/>
        </ColumnsDirective>
    </GridComponent>
    </div>)
  }
};
```

{% endtab %}

>By default, the Grid renders with **Default** mode.

## Clip Mode

The clip mode provides options to display its overflow cell content and it can be defined by the
 [`columns.clipMode`](../api/grid/column/#clipmode) property.

There are three types of [`clipMode`](../api/grid/column/#clipmode). They are:

* **Clip**: Truncates the cell content when it overflows its area.
* **Ellipsis**: Displays ellipsis when the cell content overflows its area.
* **EllipsisWithTooltip**: Displays ellipsis when the cell content overflows its area,
 also it will display the tooltip while hover on ellipsis is applied.

{% tab template="grid/autowrap", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { inventoryData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return (<div>
    <GridComponent dataSource={inventoryData} allowPaging={true}>
        <ColumnsDirective>
            <ColumnDirective field='Inventor' headerText='Name of the Inventor' clipMode='Clip' width="80"/>
            <ColumnDirective field='NumberofPatentFamilies' headerText='Number of Patent Families' clipMode='Ellipsis' width="100"/>
            <ColumnDirective field='Country' headerText='Country' width="80" />
            <ColumnDirective field='Active' headerText='Active' width="100" />
            <ColumnDirective field='Mainfieldsofinvention' headerText='Main Fields of Invention' clipMode='EllipsisWithTooltip' width="100"/>
        </ColumnsDirective>
        <Inject services={[Page]} />
    </GridComponent>
    </div>)
  }
};
```

{% endtab %}

>By default, [`columns.clipMode`](../api/grid/column/#clipmode) value is **Ellipsis**.

## See Also

* [How could I disable default behavior for all cells and for special cells in React Grid](https://www.syncfusion.com/forums/164559/how-could-i-disable-default-behavior-for-all-cells-and-for-special-cells-in-react-grid)