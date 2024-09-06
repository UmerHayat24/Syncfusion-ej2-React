---
title: "Cell"
component: "TreeGrid"
description: "Learn how to customize the Essential JS 2 TreeGrid cells with styling, text wrapping, and tooltips."
---

# Cell

## Displaying HTML Content

The HTML tags can be displayed in the TreeGrid header and content by enabling the [`disableHtmlEncode`](../api/treegrid/column/#disablehtmlencode) property.

{% tab template="treegrid/cell", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { htmlData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={htmlData} treeColumnIndex={1} childMapping='subtasks' height='300'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='<span> Task ID </span>' width='160' textAlign='Right' disableHtmlEncode={true}/>
              <ColumnDirective field='taskName' headerText='<span> Task Name </span>' width='180' disableHtmlEncode={false}/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Customize Cell Styles

The appearance of cells can be customized by using the [`queryCellInfo`](../api/treegrid/#querycellinfo) event.
The [`queryCellInfo`](../api/treegrid/#querycellinfo) event triggers for every cell. In that event handler, you can get [`QueryCellInfoEventArgs`](../api/grid/queryCellInfoEventArgs/) that contains the details of the cell.

{% tab template="treegrid/cell", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-grids';
import { Column, ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public customizeCell(args: QueryCellInfoEventArgs) {
        const cell : HTMLTableCellElement = args.cell as HTMLTableCellElement;
        if ((args.column as Column).field === 'progress' && +cell.innerHTML > 90 &&
             +cell.innerHTML <= 100) {
                cell.setAttribute('style', 'background-color:#336c12;color:white;');
        } else if (+cell.innerHTML > 20 && (args.column as Column).field === 'progress') {
            cell.setAttribute('style', 'background-color:#7b2b1d;color:white;');
        }  
    }

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='300'
            queryCellInfo={this.customizeCell}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Auto Wrap

The auto wrap allows the cell content of the treegrid to wrap to the next line when it exceeds the boundary of the cell width. The Cell Content wrapping works based on the position of white space between words.
To enable auto wrap, set the [`allowTextWrap`](../api/treegrid/#allowtextwrap) property to **true**.
You can configure the auto wrap mode by setting the [`textWrapSettings.wrapMode`](../api/treegrid/#textwrapsettings) property.

There are three types of **wrapMode**. They are:

* **Both**: This value is set by default. Auto wrap will be enabled for both the content and the header.
* **Header**: Auto wrap will be enabled only for the header.
* **Content**: Auto wrap will be enabled only for the content.

Note: When a column width is not specified, then auto wrap of columns will be adjusted with respect to the treegrid's width.

In the following example, the **textWrapSettings.wrapMode** is set to *Content*.

{% tab template="treegrid/cell", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { TextWrapSettingsModel  } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public settings: TextWrapSettingsModel = { wrapMode: 'Content' };

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='300' allowTextWrap='true' textWrapSettings={this.settings}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='90'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Custom Attributes

You can customize the treegrid cells by adding a CSS class to the [`customAttribute`](../api/treegrid/column/#customattributes) property of the column.

```CSS
.e-attr {
    background: #d7f0f4;
}
```

```typescript

    public customAttr = {class: 'e-attr'};

    <ColumnDirective
        field="taskID" headerText="Task ID" customAttributes={this.customAttr} width="90" textAlign='Right'/>
```

In the below example, we have customized the cells of *TaskID* and *StartDate* columns.

{% tab template="treegrid/cell-attribute", sourceFiles="app/App.tsx,custom.css", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import './custom.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public customAttr = {class: 'e-attr'};
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='300'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' customAttributes={this.customAttr} width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' />
              <ColumnDirective field='startDate' headerText='Start Date' customAttributes={this.customAttr} width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## TreeGrid Lines

The [`gridLines`](../api/treegrid/#gridlines) have option to display cell border and it can be defined by the
[`gridLines`](../api/treegrid/#gridlines) property.

The available modes of grid lines are:

| Modes | Actions |
|-------|---------|
| Both | Displays both the horizontal and vertical grid lines.|
| None | No grid lines are displayed.|
| Horizontal | Displays the horizontal grid lines only.|
| Vertical | Displays the vertical grid lines only.|
| Default | Displays grid lines based on the theme.|

{% tab template="treegrid/cell", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='300' gridLines='Both'>
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

>By default, the treegrid renders with **Default** mode.

## Clip Mode

The clip mode provides options to display its overflow cell content and it can be defined by the [`columns.clipMode`](../api/treegrid/column/#clipmode) property.

There are three types of [`clipMode`](../api/treegrid/column/#clipmode). They are:

* **Clip**: Truncates the cell content when it overflows its area.
* **Ellipsis**: Displays ellipsis when the cell content overflows its area.
* **EllipsisWithTooltip**: Displays ellipsis when the cell content overflows its area, also it will display the tooltip while hover on ellipsis is applied.

{% tab template="treegrid/cell", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { complexData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={complexData} treeColumnIndex={1} childMapping='subtasks' height='300' gridLines='Both'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='70' clipMode='Clip'/>
              <ColumnDirective field='assignee.firstName' headerText='Assignee' width='30' textAlign='Right' clipMode='Ellipsis' />
              <ColumnDirective field='priority' headerText='Priority' width='30' textAlign='Right' clipMode='EllipsisWithTooltip' />
              <ColumnDirective field='duration' headerText='Duration' width='30' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

>By default, [`columns.clipMode`](../api/treegrid/column/#clipmode) value is `Ellipsis`.