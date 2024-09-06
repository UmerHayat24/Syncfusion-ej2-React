---
title: "Virtualization"
component: "Grid"
description: "Learn how to improve performance in the Essential JS 2 DataGrid control by using row and column virtualization and grouping with virtualization. Also learn about the limitations of virtualization."
---

# Virtualization

Grid allows you to load large amount of data without performance degradation.

To use virtualization, you need to inject **VirtualScroll** module in grid.

## Row Virtualization

Row virtualization allows you to load and render rows only in content viewport.
It is an alternative way of paging in which the data will load while scrolling vertically.
To setup the row virtualization, you need to define
[`enableVirtualization`](../api/grid/#enablevirtualization) as **true** and
content height by [`height`](../api/grid/#height) property.

The number of records displayed in the Grid is determined implicitly by height of content area. Also you have an option to define visible number of records by [`pageSettings.pageSize`](../api/grid/pageSettingsModel/#pagesize)property.
The loaded data will be cached and reused when it is needed for next time.

{% tab template="grid/virtual-scroll", sourceFiles="app/App.tsx,app/largeData.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { PageSettingsModel, VirtualScroll, Edit, Toolbar, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './largeData';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data(1000);
  public pageSettings: PageSettingsModel = { pageSize: 50 };
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  public rules: object = { required: true };
  public render() {
    return <GridComponent dataSource={this.data} height={300} enableVirtualization={true}
            pageSettings={ this.pageSettings } editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <Inject services={[VirtualScroll, Edit, Toolbar]} />
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='100' textAlign='Right' isPrimaryKey={true} validationRules={this.rules}/>
                <ColumnDirective field='Engineer' width='100'/>
                <ColumnDirective field='Designation' width='140' editType='dropdownedit' validationRules={this.rules}/>
                <ColumnDirective field='Estimation' headerText='Estimation' textAlign='Right' width='110' editType='numericedit' validationRules={this.rules}/>
                <ColumnDirective field='Status' width='100' editType='dropdownedit'/>
            </ColumnsDirective>
            </GridComponent>
  }
}
```

{% endtab %}

## Column Virtualization

Column virtualization allows you to virtualize columns. It will render columns which are in viewport.
You can scroll horizontally to view more columns.

To setup the column virtualization, set the [`enableVirtualization`](../api/grid/#enablevirtualization) and [`enableColumnVirtualization`](../api/grid/#enablecolumnvirtualization) properties as **true**.

{% tab template="grid/virtual-scroll", sourceFiles="app/App.tsx,app/virtualdata.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, VirtualScroll, Edit, Toolbar, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { dataSource } from './virtualData';

export default class App extends React.Component<{}, {}>{
  
  public data: object[] = dataSource();
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  public rules: object = { required: true };
  public render() {
    return <GridComponent dataSource={this.data} height={300} enableVirtualization={true}
            enableColumnVirtualization={true} pageSettings={{ pageSize: 50 }} editSettings={this.editOptions} toolbar={this.toolbarOptions}>
            <Inject services={[VirtualScroll, Edit, Toolbar]} />
            <ColumnsDirective>
                <ColumnDirective field='SNo' headerText='S.No' width='120' isPrimaryKey={true} validationRules={this.rules}/>
                <ColumnDirective field='FIELD1' headerText='Player Name' width='140' editType='dropdownedit' validationRules={this.rules}/>
                <ColumnDirective field='FIELD2' headerText='Year' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD3' headerText='Stint' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD4' headerText='TMID' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD5' headerText='LGID' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD6' headerText='GP' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD7' headerText='GS' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD8' headerText='Minutes' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD9' headerText='Points' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD10' headerText='oRebounds' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD11' headerText='dRebounds' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD12' headerText='Rebounds' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD13' headerText='Assists' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD14' headerText='Steals' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD15' headerText='Blocks' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD16' headerText='Turnovers' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD17' headerText='PF' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD18' headerText='fgAttempted' width='150' textAlign='Right'/>
                <ColumnDirective field='FIELD19' headerText='fgMade' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD20' headerText='ftAttempted' width='150' textAlign='Right'/>
                <ColumnDirective field='FIELD21' headerText='ftMade' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD22' headerText='ThreeAttempted' width='150' textAlign='Right'/>
                <ColumnDirective field='FIELD23' headerText='ThreeMade' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD24' headerText='PostGP' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD25' headerText='PostGS' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD26' headerText='PostMinutes' width='120' textAlign='Right'/>
                <ColumnDirective field='FIELD27' headerText='PostPoints' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD28' headerText='PostoRebounds' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD29' headerText='PostdRebounds' width='130' textAlign='Right'/>
                <ColumnDirective field='FIELD30' headerText='PostRebounds' width='130' textAlign='Right' editType='numericedit' validationRules={this.rules}/>
            </ColumnsDirective>
            </GridComponent>
  }
};
```

{% endtab %}

> Column's [`width`](../api/grid/column/#width) is required for column virtualization.
If column's width is not defined then Grid will consider its value as **200px**.

## Virtualization with Grouping

Both the row and column virtualization can be used along with grouping. At initial rendering, the virtual height of scrollbar will be set based on the total number of records and after grouping, it will be refreshed based on the grouped state(expand/collapse). While collapse the group caption row in current viewport then the next view page grouped records are shown.

> The collapsed/expanded state will persist only for local dataSource while scrolling.

## Limitations for Virtualization

* While using column virtualization, column width should be in the pixel. Percentage values are not accepted.
* Due to the element height limitation in browsers, the maximum number of records loaded by the grid is limited by the browser capability.
* Cell selection will not be persisted in both row and column virtualization.
* Virtual scrolling is not compatible with batch editing, detail template and hierarchy features.
* Group expand and collapse state will not be persisted.
* Since data is virtualized in grid, the aggregated information and total group items are displayed based on the current view items. To get these information regardless of the view items, refer to the [`Group with Page`](./grouping/#group-with-paging) topic.
* The page size provided must be two times larger than the number of visible rows in the grid.
If the page size is failed to meet this condition then the size will be determined by grid.
* The height of the grid content is calculated using the row height and
total number of records in the data source and hence features which changes row height such as text wrapping are not supported.
If you want to increase the row height to accommodate the content then
you can specify the row height as below to ensure all the table rows are in same height.

```css
.e-grid .e-row {
    height: 2em;
}
```

* Programmatic selection using the [`selectRows`](../api/grid/#selectrows) method is not supported in virtual scrolling.