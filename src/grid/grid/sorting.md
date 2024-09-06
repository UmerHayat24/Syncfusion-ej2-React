---
title: "Sorting"
component: "Grid"
description: "Learn how to sort rows in the Essential JS 2 DataGrid control, perform initial sorting, multi-column sorting and customize sorting logic."
---

# Sorting

The Grid component has support to sort data bound columns in **Ascending** or **Descending** order.
This can be achieved by setting [`allowSorting`](../api/grid/#allowsorting) property as true.

To dynamically sort a particular column, click on its column header.
The order switch between **Ascending** and **Descending** each time you click a column header for sorting.

To use Sorting, inject **Sort** module in Grid.

{% tab template="grid/sort", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Sort,  } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} allowSorting={true} height={270}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Sort]} />
    </GridComponent>
  }
};
```

{% endtab %}

> * Grid column sorted in **Ascending** order. If you click on already sorted column, Grid toggles the sort direction.
> * You can apply and clear sorting by invoking [`sortColumn`](../api/grid/#sortcolumn) and
[`clearSorting`](../api/grid/#clearsorting) methods.
> * To disable Sorting for a particular column, by specifying [`columns.allowSorting`](../api/grid/column/#allowsorting) to **false**.

## Initial Sort

To apply sort at initial rendering, set the [`field`](../api/grid/sortDescriptorModel/#field) and
[`direction`](../api/grid/sortDescriptorModel/#direction) in [`sortSettings.columns`](../api/grid/sortSettingsModel/#columns).

{% tab template="grid/sort", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public sortingOptions: SortSettingsModel = {
    columns: [{ field: 'EmployeeID', direction: 'Ascending' }]
  };
  public render() {
      return <GridComponent dataSource={data} allowSorting={true} sortSettings={this.sortingOptions}
          height={270}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Sort]} />
      </GridComponent>
  }
};
```

{% endtab %}

## Multi-column sorting

You can sort more than one column in a Grid. To sort multiple columns, press and hold the **CTRL** key and click the column header. The sorting order will be displayed in the header while performing multi-column sorting.

To clear sorting for a particular column, press the **Shift + mouse left click**.

> The [`allowSorting`](../api/grid/#allowsorting) must be true while enabling multi-column sort.
> Set [`allowMultiSorting`](../api/grid/#allowmultisorting) property as **false** to disable multi-column sorting.

{% tab template="grid/sort", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} allowSorting={true} allowMultiSorting={true} height={270}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Sort]} />
    </GridComponent>
  }
};
```

{% endtab %}

## Sort order

By default, the sorting order will be as **ascending -> descending -> none**.

When first click a column header it sorts the column in ascending. Again click the same column header, it will sort the column in descending. A repetitive third click on the same column header will clear the sorting.

## Sort foreign key column based on Text

For local data in Grid, sorting will be performed based on the [`foreignKeyValue`](../api/grid/column/#foreignkeyvalue).

For remote data in Grid, sorting will be performed based on the [`foreignKeyField`](../api/grid/column/#foreignkeyfield), we need to handle the sorting operation at the server side.

```typescript
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, ForeignKey, GridComponent, Inject, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
        adaptor: new ODataV4Adaptor,
        url:'/OData/Items'
    });
    public employeeData = new DataManager({
        adaptor: new ODataV4Adaptor,
        url:'/OData/Brands'
    });
    public render() {
        return <GridComponent dataSource={this.data} height={315}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
                <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName'
                    foreignKeyField='EmployeeID' dataSource={this.employeeData}  headerText='Employee Name' width='150'/>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
            </ColumnsDirective>
            <Inject services={[ForeignKey,Sort]} />
        </GridComponent>
    }
};
```

The following code example describes the handling of sorting operation at the server side.

```cs
    public class ItemsController : ODataController
    {
        [EnableQuery]
        public IQueryable<Item> Get()
        {
            List<Item> GridData = JsonConvert.DeserializeObject<Item[]>(Properties.Resources.ItemsJson).AsQueryable().ToList();
            List<Brand> empData = JsonConvert.DeserializeObject<Brand[]>(Properties.Resources.BrandsJson).AsQueryable().ToList();
            var queryString = HttpContext.Current.Request.QueryString;
            var allUrlKeyValues = ControllerContext.Request.GetQueryNameValuePairs();
            string key = allUrlKeyValues.LastOrDefault(x => x.Key == "$orderby").Value;
            if (key != null)
            {
                if (key == "EmployeeID") {
                    GridData = SortFor(key); //Only for foreignKey Column ascending
                }
                else if(key == "EmployeeID desc") {
                    GridData = SortFor(key); //Only for foreignKey Column descending
                }
            }
            var count = GridData.Count();
            var data = GridData.AsQueryable();
            return data;
        }

        public List<Item> SortFor(String Sorted)
        {
            List<Item> GridData = JsonConvert.DeserializeObject<Item[]>(Properties.Resources.ItemsJson).AsQueryable().ToList();
            List<Brand> empData = JsonConvert.DeserializeObject<Brand[]>(Properties.Resources.BrandsJson).AsQueryable().ToList();
            if (Sorted == "EmployeeID") //check whether ascending or descending
                empData = empData.OrderBy(e => e.FirstName).ToList();
            else if(Sorted == "EmployeeID desc")
                empData = empData.OrderByDescending(e => e.FirstName).ToList();
            List<Item> or = new List<Item>();
            for (int i = 0; i < empData.Count(); i++) {
                //Select the Field matching records
                IEnumerable<Item> list = GridData.Where(pred => pred.EmployeeID == empData[i].EmployeeID).ToList();
                or.AddRange(list);
            }
            return or;
        }
    }
```

## Sorting Events

During the sort action, the Grid component triggers two events. [`actionBegin`](../api/grid/#actionbegin) event triggers before the sort action starts, and [`actionComplete`](../api/grid/#actioncomplete) event triggers after the sort action complete. Using these events you can perform the needed actions.

{% tab template="grid/sort", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ActionEventArgs, ColumnDirective, ColumnsDirective, GridComponent, Inject, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public actionHandler (args: ActionEventArgs) {
      /** Custom Action */
      alert(args.requestType + ' ' + args.type);
  }
  public render() {
      return <GridComponent dataSource={data} allowSorting={true} height={315} actionBegin={this.actionHandler}
          actionComplete={this.actionHandler}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Sort]} />
      </GridComponent>
  }
};
```

{% endtab %}

> [`args.requestType`](../api/grid/sortEventArgs/#requesttype) retrieves the current action name.
For example in sorting, the [`args.requestType`](../api/grid/sortEventArgs/#requesttype) value is **sorting**.

## Custom sort comparer

You can customize the default sort action for a column by defining the [`column.sortComparer`](../api/grid/column/#sortcomparer) property.
The sort comparer function has the same functionality like
[`Array.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sort comparer.

In the following example, custom sort comparer function was defined in the **Customer ID** column.

{% tab template="grid/sort", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{

    /** Custom comparer function */
    public sortComparer(reference: string, comparer:  string) {
        if (reference < comparer) {
            return -1;
        }
        if (reference > comparer) {
            return 1;
        }
        return 0;
    };

    public render() {
        return <GridComponent dataSource={data} height={315} allowSorting={true}>
            <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
                <ColumnDirective field='CustomerID' sortComparer={this.sortComparer} headerText='Customer ID' width='150'/>
                <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
            </ColumnsDirective>
            <Inject services={[Sort]} />
        </GridComponent>
    }
};
```

{% endtab %}

> The sort comparer function will work only for the local data.

## Touch Interaction

When you tap the grid header on touchscreen devices, the selected column header is sorted. A popup ![Sorting](images/sorting.jpg) is displayed for multi-column sorting.
To sort multiple columns, tap the popup![Multi Sorting](images/msorting.jpg), and then tap the desired grid headers.

 The [`allowMultiSorting`](../api/grid/#allowmultisorting) and [`allowSorting`](../api/grid/#allowsorting) should be **true** then only the popup will be shown.

The following screenshot shows grid touch sorting.

![Touch Interaction](images/touch-sorting.jpg)
