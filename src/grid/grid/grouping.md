---
title: "Grouping"
component: "Grid"
description: "Learn how to group rows, apply initial groups, customize caption templates, and group by format in the Essential JS 2 DataGrid control."
---

# Grouping

The Grid has options to group records by dragging and dropping the column header to the group drop area.
When grouping is applied, grid records are organized into a hierarchical structure to facilitate easier expansion and collapse of records.

To enable grouping in the grid, set the [`allowGrouping`](../api/grid/#allowgrouping) as true.
Grouping options can be configured through the [`groupSettings`](../api/grid/groupSettings/).

To Group, inject **Group** module in the grid.

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Group, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render(){
    return <GridComponent  dataSource={data} allowGrouping={true} height={267}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
            </ColumnsDirective>
            <Inject services={[Group]}/>
        </GridComponent >
    }
};
```

{% endtab %}

> * You can group and ungroup columns by using the [`groupColumn`](../api/grid/group/#groupcolumn) and [`ungroupColumn`](../api/grid/group/#ungroupcolumn) methods.
> * To disable grouping for a particular column, set the [`columns.allowGrouping`](../api/grid/column/#allowgrouping) to **false**.

## Initial group

To apply group at initial rendering, set the column field name in the [`groupSettings.columns`](../api/grid/groupSettingsModel/#columns).

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions : GroupSettingsModel = {
    columns: ['CustomerID', 'ShipCity']
  };

  public render(){
      return <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions} height={267}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent >
      }
};
```

{% endtab %}

## Caption Template

You can customize the group caption by using the [`groupSettings.captionTemplate`](../api/grid/groupSettings/#captionTemplate) property.

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions : GroupSettingsModel = {
    columns: ['CustomerID', 'ShipCity'],
    showDropArea: false,
    captionTemplate: '<span class="groupItems" style="color:blue"> ${field} - ${count} Items</span>'
  };

  public render(){
      return <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions} height={267}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent >
      }
};
```

{% endtab %}

## Hide drop area

To avoid ungrouping or further grouping of a column after initial column
grouping, define the [`groupSettings.showDropArea`](../api/grid/groupSettings/#showdroparea) as **false**.

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions : GroupSettingsModel = {
    columns: ['CustomerID', 'ShipCity'],
    showDropArea: false
  };

  public render(){
      return <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions} height={267}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent >
      }
};
```

{% endtab %}

## Group with Paging

On grouping columns with paging feature, the aggregated information and total items are displayed based on the current page.
The grid does not consider aggregated information and total items from other pages.
To get additional details (aggregated information and total items) from other pages, set the
[`groupSettings.disablePageWiseAggregates`](../api/grid/groupSettings/#disablepagewiseaggregates) to false.

> If remote data is bound to grid dataSource, two requests will be sent when performing grouping action; one for getting the grouped data and another for getting aggregate details and total items count.

## Group by format

By default, columns will be grouped by the data or value present for the particular row. To group numeric
or datetime column based on the mentioned format, you have to enable the
[`enableGroupByFormat`](../api/grid/column/#enablegroupbyformat) property of the corresponding
grid columns.

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions : GroupSettingsModel = {
    columns: ['OrderDate', 'Freight'],
    showDropArea: false
  };

  public render(){
      return <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions} height={315}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='OrderDate' headerText='Order Date' format='yMMM' enableGroupByFormat={true} width='150'/>
                  <ColumnDirective field='Freight' headerText='Freight' format='C2' enableGroupByFormat={true} width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent >
      }
};
```

{% endtab %}

## Grouping events

During the group action, the grid component triggers two events. The [`actionBegin`](../api/grid/#actionbegin) event triggers before the group action starts and the [`actionComplete`](../api/grid/#actioncomplete) event triggers after the group action is completed. Using these events you can perform any action.

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ActionEventArgs, ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions : GroupSettingsModel = { columns: ['CustomerID'] };
  public actionHandler (args: ActionEventArgs) {
      /** Custom Action */
      alert(args.requestType + ' ' + args.type);
  }

  public render(){
      return (<div>
              <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions}
              actionBegin={this.actionHandler} actionComplete={this.actionHandler} height={280}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent ></div>)
      }
};
```

{% endtab %}

> [`args.requestType`](../api/grid/sortEventArgs/#requesttype) retrieves current action name.
For example in grouping, the [`args.requestType`](../api/grid/sortEventArgs/#requesttype) value is **grouping**.

## Collapse By External Button

You can collapse the selected group from an external button by invoking [`expandCollapseRows`](../api/grid/group/#expandcollapserows) method.

{% tab template="grid/group", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Grid, GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public groupOptions : GroupSettingsModel = {
    columns: ['CustomerID']
  };
  public collapse() {
      if (this.grid) {
        if (this.grid.getSelectedRowIndexes().length) {
          let currentTr: HTMLElement = this.grid.getRows()[this.grid.getSelectedRowIndexes()[0]] as HTMLElement;
          while (currentTr.classList && currentTr.classList.length){
              currentTr = currentTr.previousSibling as HTMLElement;
          }
          const collapseElement = currentTr.querySelector('.e-recordplusexpand');
          /** Pass the collapse row element */
          this.grid.groupModule.expandCollapseRows(collapseElement as Element);
        }
      }
  }

  public render(){
      this.collapse = this.collapse.bind(this);
      return (<div>
              <ButtonComponent className= {'e-flat'} onClick= { this.collapse }>Collapse</ButtonComponent>
              <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions}
                height={240} ref={g=> this.grid = g}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent ></div>)
      }
};
```

{% endtab %}

## Reordering on Grouped Columns

Grid provides an option to interchange the position of the Grouped Columns by dragging and dropping the grouped headercells in the droparea. So, any new column entering into the droparea can also be dropped in any position.

To enable this feature, you have to set the [`groupSettings.allowReordering`](../api/grid/groupSettings/#allowReordering) property as **true**.

{% tab template="grid/group-reorder", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Grid, GridComponent, Group, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public groupOptions : GroupSettingsModel = {
    columns: ['CustomerID'],
    allowReordering: true
  };

  public render(){
      return (<div>
              <GridComponent  dataSource={data} allowGrouping={true} groupSettings={this.groupOptions}
                height={240} ref={g=> this.grid = g}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Group]}/>
          </GridComponent ></div>)
      }
};
```

{% endtab %}

## Lazy Load Grouping

The lazy load grouping allows you to load grouped records to the Grid through the on-demand concept. So, you can use this feature to load a huge amount of grouped data to the Grid without any performance degradation.

When you enable this feature, the Grid will render only the initial level caption rows in the collapsed state at grouping. The child rows of each caption will be fetched from the server and render in the Grid when you expand the caption row. The fetching child records count will be implicitly determined by the content area occupying rows count. So, if the child records exceed the count, then the Grid will request the server again to fetch the next block of child records on scrolling.

The caption row expand/collapse state will be persisted on paging and Grid pages count will be determined based on the caption rows count instead of the child rows.

To enable this feature, you have to set the [`groupSettings.enableLazyLoading`](../api/grid/groupSettings/#enableLazyLoading) property as **true**.

{% tab template="grid/lazy-load-grouping", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Grid, GridComponent, Group, Page, LazyLoadGroup, GroupSettingsModel, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public groupOptions : GroupSettingsModel = {
    enableLazyLoading: true,
    columns: ['ProductName', 'CustomerName']
  }

  public render(){
      return (<div>
              <GridComponent dataSource={data} allowPaging={true} allowGrouping={true} groupSettings={this.groupOptions}
                height={240} ref={g=> this.grid = g}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' textAlign="Right" width='120'/>
                  <ColumnDirective field='ProductName' headerText='Product Name' width='160'/>
                  <ColumnDirective field='ProductID' headerText='Product ID' textAlign="Right" width='120'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
                  <ColumnDirective field='CustomerName' headerText='Customer Name' width='160'/>
              </ColumnsDirective>
              <Inject services={[Page, Group, LazyLoadGroup]}/>
          </GridComponent></div>)
      }
};
```

{% endtab %}

### Handling the lazy load grouping at server-side

You can use the [`UrlAdaptor`](../../data/adaptors.html#url-adaptor) of `DataManager` when binding the remote data. Along with the default server request, this feature will additionally send the below details to handle the lazy load grouping. In the server end, these details are bound with the `IsLazyLoad` and `OnDemandGroupInfo` parameters in the `DataManagerRequest` model. Please refer to the below table and screenshots.

Property Name |Description
-----|-----
`isLazyLoad` |To differentiate the default grouping and lazy load grouping
`onDemandGroupInfo` |Have the details of expanded caption row grouping `level`, `skip`, `take` and `filter` query of the child records

![IsLazyLoad](images/islazyload.jpg)

![OnDemandGroupInfo](images/groupinfo.jpg)

The following code example describes the lazy load grouping handled at the server-side with other the grid actions.

```typescript
public IActionResult UrlDatasource([FromBody] DataManagerRequest dm)
{
    IEnumerable groupedData = null;
    IEnumerable<Customers> DataSource = customers;
    DataOperations operation = new DataOperations();

    if (dm.Search != null && dm.Search.Count > 0)
    {
        DataSource = operation.PerformSearching(DataSource, dm.Search);  //Search
    }
    if (dm.Sorted != null && dm.Sorted.Count > 0) //Sorting
    {
        DataSource = operation.PerformSorting(DataSource, dm.Sorted);
    }
    if (dm.Where != null && dm.Where.Count > 0) //Filtering
    {
        DataSource = operation.PerformFiltering(DataSource, dm.Where, dm.Where[0].Operator);
    }
    int count = DataSource.Cast<Customers>().Count();
    if (dm.IsLazyLoad == false && dm.Skip != 0)
    {
        DataSource = operation.PerformSkip(DataSource, dm.Skip); // Paging
    }
    if (dm.IsLazyLoad == false && dm.Take != 0)
    {
        DataSource = operation.PerformTake(DataSource, dm.Take);
    }
    if (dm.IsLazyLoad)
    {
        groupedData = operation.PerformGrouping<Customers>(DataSource, dm); // Lazy load grouping
        if (dm.OnDemandGroupInfo != null && dm.Group.Count() == dm.OnDemandGroupInfo.Level)
        {
            count = groupedData.Cast<Customers>().Count();
        }
        else
        {
            count = groupedData.Cast<Group>().Count();
        }
        groupedData = operation.PerformSkip(groupedData, dm.OnDemandGroupInfo == null ? dm.Skip : dm.OnDemandGroupInfo.Skip);
        groupedData = operation.PerformTake(groupedData, dm.OnDemandGroupInfo == null ? dm.Take : dm.OnDemandGroupInfo.Take);
    }
return dm.RequiresCounts ? Json(new { result = groupedData == null ? DataSource : groupedData, count = count }) : Json(DataSource);
}

```

### Limitations for Lazy load grouping

* Due to the element height limitation in browsers, the maximum number of records loaded by the grid is limited due to the browser capability.
* DataManager's [`UrlAdaptor`](../../data/adaptors.html#url-adaptor) and `JsonAdaptor` only have the built-in lazy load grouping support.
* Lazy load grouping is not compatible with virtualization, infinite scroll and batch editing, row template etc.
* Programmatic selection is not supported.

## See Also

* [Exporting grouped records](./excel-exporting#exporting-grouped-records)
* [Is there a way to include the template in the Group summary in React Grid?](https://www.syncfusion.com/forums/150662/is-there-a-way-to-include-the-template-in-the-group-summary-in-react-grid)
* [How to customize the grouping row data in React Grid](https://www.syncfusion.com/forums/151019/how-to-customize-the-grouping-row-data-in-react-grid)