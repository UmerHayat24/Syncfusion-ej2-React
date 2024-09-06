---
title: "Filtering"
component: "Grid"
description: "Learn how to filter rows in the DataGrid using the filter bar, menu, and Excel-like filtering. Also learn how to use custom filter components in the Essential JS 2 DataGrid control."
---

# Filtering

Filtering allows you to view particular records based on filter criteria. To enable filtering in the Grid,
set the [`allowFiltering`](../api/grid/#allowfiltering) to true.
Filtering options can be configured through [`filterSettings`](../api/grid/filterSettings/).

To use filter, inject the **Filter** module in the grid.

To learn about how to work with Filtering Options, you can check on this video for React Grid.

`youtube:UQmuY9D0efQ`

<!---
The Grid supports two types of filter, they are
* Filter bar
* Excel
-->

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} allowFiltering={true} height={273}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Filter]} />
    </GridComponent>
  }
};
```

{% endtab %}

> * You can apply and clear filtering, by using [`filterByColumn`](../api/grid/filter/#filterbycolumn) and [`clearFiltering`](../api/grid/filter/#clearfiltering) methods.
> * To disable Filtering for a particular column, by specifying
[`columns.allowFiltering`](../api/grid/column/#allowfiltering) to **false**.

## Initial filter

To apply the filter at initial rendering, set the filter [`predicate`](../api/grid/predicate/) object in [`filterSettings.columns`](../api/grid/filterSettingsModel/#columns).

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public filterOptions: FilterSettingsModel = {
    columns: [
      { field: 'ShipCity', matchCase: false,
        operator: 'startswith', predicate: 'and', value: 'reims'
      },
      { field: 'ShipName', matchCase: false, operator: 'startswith',
        predicate: 'and', value: 'Vins et alcools Chevalier'
      }
    ]
  };
  public render() {
      return <GridComponent dataSource={data} allowFiltering={true} filterSettings={this.filterOptions}
          height={273}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCity' width='100'/>
              <ColumnDirective field='ShipName' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

## Filter operators

The filter operator for a column can be defined in [`filterSettings.columns.operator`](../api/grid/predicateModel/#operator) property.

The available operators and its supported data types are,

Operator |Description |Supported Types
-----|-----|-----
startswith |Checks whether a value begins with the specified value. |String
endswith |Checks whether a value ends with specified value. |String
contains |Checks whether a value contains with specified value. |String
equal |Checks whether a value equal to specified value. |String &#124; Number &#124; Boolean &#124; Date
notequal |Checks whether a value not equal to specified value. |String &#124; Number &#124; Boolean &#124; Date
greaterthan |Checks whether a value is greater than with specified value. |Number &#124; Date
greaterthanorequal|Checks whether a value is greater than or equal to specified value. |Number &#124; Date
lessthan |Checks whether a value is less than with specified value. |Number &#124; Date
lessthanorequal |Checks whether a value is less than or equal to specified value. |Number &#124; Date

## Filter bar

By defining the [`allowFiltering`](../api/grid/#allowfiltering) to **true**, then filter bar row will be rendered next to header which allows you to filter data. You can filter the records with different expressions depending upon the column type.

 **Filter bar Expressions:**

 You can enter the following filter expressions(operators) manually in the filter bar.

Expression |Example |Description |Column Type
-----|-----|-----|-----
= |=value |equal |Numeric
!= |!=value |notequal |Numeric
> |>value |greaterthan |Numeric
< |<value |lessthan |Numeric
>= |>=value |greaterthanorequal |Numeric
<=|<=value|lessthanorequal |Numeric
* |*value |startswith |String
% |%value |endswith |String
N/A |N/A |Always **equal** operator will be used for Date filter |Date
N/A |N/A |Always **equal** operator will be used for Boolean filter |Boolean

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} allowFiltering={true} height={273}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Filter]} />
    </GridComponent>
  }
};
```

{% endtab %}

> By default, the [`filterSettings.columns.operator`](../api/grid/predicateModel/#operator) value is **equal**.

## Filter bar template with custom component

The [`filterBarTemplate`](../api/grid/column/#filterbartemplate) is used to add a custom component for a particular column and this contains the following functions.

* **create** – It is used for creating custom components.
* **write** - It is used to perform filtering actions on Grid from custom components.

In the following sample dropdown is used  as custom component in **EmployeeID** column.

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { Column, ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, Grid, GridComponent, IFilterUI, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public templateOptions: IFilterUI = {
      create: (args: { element: Element, column: Column }) => {
          const dd: HTMLSelectElement = document.createElement('select');
          dd.id = 'EmployeeID';
          dd.style.width = '100%';
          const dataSource: string[]= ['All','1','3','4','5','6','8','9'];
          for(const d of dataSource){
              const option: HTMLOptionElement = document.createElement('option');
              option.value = d
              option.innerHTML = d;
              dd.appendChild(option);
          }
          return dd;
      },
      write: (args: { element: Element, column: Column }) => {
          args.element.addEventListener('input', (arg: MouseEvent)  => {
              if (this.grid && arg.currentTarget) {
                const elem: HTMLSelectElement = arg.currentTarget as HTMLSelectElement;
                if(elem.value !== 'All') {
                  const value: number = +elem.value;
                  this.grid.filterByColumn(elem.id, 'equal', value);
                } else {
                    this.grid.removeFilteredColsByField(elem.id);
                }
              }
          });
      },
  };
  public render() {
      return <GridComponent dataSource={data} allowFiltering={true} height={273} ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100' />
              <ColumnDirective field='EmployeeID' width='100' filterBarTemplate={this.templateOptions} textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

## Filter menu

You can enable filter menu by setting the [`filterSettings.type`](../api/grid/filterSettings/#type) as **Menu**.
The filter menu UI will be rendered based on its column type, which allows you to filter data.
You can filter the records with different operators.

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public FilterOptions: FilterSettingsModel = {
    type: 'Menu'
  };
  public render() {
      return <GridComponent dataSource={data} filterSettings={this.FilterOptions} allowFiltering={true}
              height={273}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

> * [`allowFiltering`](../api/grid/#allowfiltering) must be set as true to enable filter menu.
> * Setting [`columns.allowFiltering`](../api/grid/column/#allowfiltering) as false will prevent
 filter menu rendering for a particular column.

### Custom component in filter menu

The [`column.filter.ui`](../api/grid/column/#filter) is used to add custom filter components to a particular column.
To implement custom filter ui, define the following functions:

* **create**:  Use for creating custom component.
* **write**: Wire events for custom component.
* **read**: Read the filter value from custom component.

In the following sample, dropdown is used  as custom component in the OrderID column.

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import { DataManager } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, GridComponent, IFilter, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public FilterOptions: FilterSettingsModel = {
    type: 'Menu'
  };
  public dropInstance: DropDownList;
  public Filter : IFilter = {
  ui: {
      create: (args: { target: Element, column: object }) => {
          const flValInput: HTMLElement = createElement('input', { className: 'flm-input' });
          args.target.appendChild(flValInput);
          this.dropInstance = new DropDownList({
              dataSource: new DataManager(data),
              fields: { text: 'OrderID', value: 'OrderID' },
              placeholder: 'Select a value',
              popupHeight: '200px'
          });
          this.dropInstance.appendTo(flValInput);
      },
      read: (args: { target: Element, column: any, operator: string, fltrObj: Filter }) => {
          args.fltrObj.filterByColumn(args.column.field, args.operator, this.dropInstance.value);
          },
      write: (args: {
          column: object, target: Element, parent: any,
          filteredValue: number | string }) => {
              this.dropInstance.value = args.filteredValue;
          }
      }
  }
  public render() {
      return <GridComponent dataSource={data} filterSettings={this.FilterOptions} allowFiltering={true} height={273}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' filter={this.Filter} width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

### Enable different filter for a column

You can use both **Menu** and **CheckBox** filter in a same Grid. To do so, set the
[`column.filter.type`](../api/grid/column/#filter) as **Menu** or **CheckBox**.

In the following sample menu filter is enabled by default and checkbox filter is enabled for the CustomerID column using the
[`column.filter.type`](../api/grid/column/#filter).

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, GridComponent, IFilter, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public FilterOptions: FilterSettingsModel = {
    type: 'Menu'
  };
  public Filter : IFilter = {
    type: 'CheckBox'
  }
  public render() {
      return <GridComponent dataSource={data} filterSettings={this.FilterOptions}
            allowFiltering={true} height={273}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' filter={this.Filter} width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

## Filter template

Filter template provides an option to use the custom filter UI for a particular column by using the [`columns.filterTemplate`](../api/grid/column/#filtertemplate) property. The custom filter UI provided by [`columns.filterTemplate`](../api/grid/column/#filtertemplate) can be used by the filter bar, menu, and advanced filter from an excel filter.

> The [`columns.filterTemplate`](../api/grid/column/#filtertemplate) property value should be a React functional component.

### Filter Bar

You can customize default filter bar component of a column by custom component using [`filter template`](../api/grid/column/#filtertemplate).

The following example demonstrates the way to use filter template for a column when using filter bar. In the following example, the **DropdownList** component is used to filter **CustomerID** column using filter template.

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { DataUtil } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, Grid, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public dropdata: string[] = DataUtil.distinct(data, 'CustomerID') as string[];
  public filterTemplate(props:any): any {
      this.dropdata.push('Clear');
      return (<DropDownListComponent id={props.column.field} popupHeight='250px' dataSource={this.dropdata} change={this.onChange} /> );
  }
  public onChange(args: any): any{
    if (this.grid) {
      if (args.value === 'Clear') {
        this.grid.clearFiltering();
      } else {
        this.grid.filterByColumn('CustomerID', 'equal', args.value);
      }
    }
  }
  public render() {
      this.filterTemplate = this.filterTemplate.bind(this);
      this.onChange = this.onChange.bind(this);
      return <GridComponent ref={g => this.grid = g} dataSource={data} allowFiltering={true} >
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign="Right"/>
              <ColumnDirective field='EmployeeID' headerText='EmployeeID' width='140' textAlign="Right"/>
              <ColumnDirective field='CustomerID' filterTemplate={this.filterTemplate} width='140'/>
              <ColumnDirective field='ShipName' width='170' textAlign="Right"/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

### Filter Menu

You can customize default filter menu component of a column by custom component using [`filter template`](../api/grid/column/#filtertemplate).

The following example demonstrates the way to use filter template for a column when using filter menu. In the following example, the **DropdownList** component is used to filter **ShipName** column using filter template.

<!--{% tab template="grid/filter", sourceFiles="app/App.tsx" %}-->

```typescript
import { DataUtil } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ColumnDirective, ColumnsDirective, FilterSettingsModel } from '@syncfusion/ej2-react-grids';
import { Filter, Grid, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public fields: object = { text: 'CustomerID', value: 'CustomerID' };
  public filterOptions: FilterSettingsModel = {
     type: 'Menu'
  };
  public dropdata: string[] = DataUtil.distinct(data, 'CustomerID') as string[];
  public filterTemplate(props:any): any {
      return (<DropDownListComponent id={props.column.field} value={props.CustomerID}popupHeight='250px'
      fields={this.fields} dataSource={this.dropdata} /> );
  }
  public render() {
      this.filterTemplate = this.filterTemplate.bind(this);
      return <GridComponent ref={g => this.grid = g} dataSource={data} filterSettings={this.filterOptions} allowFiltering={true} >
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign="Right"/>
              <ColumnDirective field='EmployeeID' headerText='EmployeeID' width='140' textAlign="Right"/>
              <ColumnDirective field='CustomerID' filterTemplate={this.filterTemplate} width='140'/>
              <ColumnDirective field='ShipName' width='170' textAlign="Right"/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

<!--{% endtab %}-->

### Excel Filter

You can use the [`columns.filterTemplate`](../api/grid/column/#filtertemplate) property to define custom component in advanced filter UI from excel filter for a particular column.

The following example demonstrates the way to use filter template for a column when using excel filter. In the following example, the **DropdownList** component is used to filter **CustomerID** column using filter template.

{% tab template="grid/filter", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { DataUtil } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ColumnDirective, ColumnsDirective, FilterSettingsModel } from '@syncfusion/ej2-react-grids';
import { Filter, Grid, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public fields: object = { text: 'CustomerID', value: 'CustomerID' };
  public filterOptions: FilterSettingsModel = {
     type: 'Excel'
  };
  public dropdata: string[] = DataUtil.distinct(data, 'CustomerID') as string[];
  public filterTemplate(props:any): any {
      const val = isNullOrUndefined(props.CustomerID) ? '' : props.CustomerID;
      return (<DropDownListComponent id='CustomerID' value={val} popupHeight='250px'
      fields={this.fields} dataSource={this.dropdata} /> );
  }
  public render() {
      this.filterTemplate = this.filterTemplate.bind(this);
      return <GridComponent ref={g => this.grid = g} dataSource={data} filterSettings={this.filterOptions} allowFiltering={true} >
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign="Right"/>
              <ColumnDirective field='EmployeeID' headerText='EmployeeID' width='140' textAlign="Right"/>
              <ColumnDirective field='CustomerID' filterTemplate={this.filterTemplate} width='140'/>
              <ColumnDirective field='ShipName' width='170' textAlign="Right"/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

> * By default, while opening the excel/checkbox filter in the Grid, the filter dialog will get and display the distinct data from the first 1000 records bound to the Grid to optimize performance. The remaining records will be returned as a result of the search option of the filter dialog.
> * However, we can increase the excel/checkbox filter count by modifying the `filterChoiceCount` argument value(as per our need) in the [`actionBegin`](../api/grid/#actionBegin) event when the [`requestType`](../api/grid/filterEventArgs/#requesttype) is `filterchoicerequest` or `filtersearchbegin`. This is demonstrated in the below code snippet,

```typescript
public actionBegin(args: FilterEventArgs) {
    if (args.requestType === "filterchoicerequest" || args.requestType === "filtersearchbegin") {
        args.filterChoiceCount = 3000;
    }
}
```

### Template Context

The filter template should be a React Component. You can access the column information inside the component.

The following properties will be available at the time of template execution.

| Property Name | Usage |
|---------------|--------|
| <kbd>column</kbd> | Get the current column information.|

In the below code example, we have enabled the DropDownList which is used as filter UI for **CustomerID** column based on the [`columns.allowFiltering`](../api/grid/column/#allowfiltering) property.

```typescript
export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public dropdata: string[] = DataUtil.distinct(data, 'CustomerID') as string[];
  public filterTemplate(props:any): any {
      this.dropdata.push('Clear');
      /** The enabled attributes will be added based on the column property. */
      return (<DropDownListComponent enabled={props.column.allowFiltering} id={props.column.field}popupHeight='250px'
      dataSource={this.dropdata} change={this.onChange} /> );
  }
  public onChange(args: any): any{
    if (this.grid) {
      if (args.value === 'Clear') {
        this.grid.clearFiltering();
      } else {
        this.grid.filterByColumn('CustomerID', 'equal', args.value);
      }
    }
  }
  public render() {
      this.filterTemplate = this.filterTemplate.bind(this);
      this.onChange = this.onChange.bind(this);
      return <GridComponent ref={g => this.grid = g} dataSource={data} allowFiltering={true} >
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign="Right"/>
              <ColumnDirective field='EmployeeID' headerText='EmployeeID' width='140' textAlign="Right"/>
              <ColumnDirective field='CustomerID' allowFiltering={false} filterTemplate={this.filterTemplate} width='140'/>
              <ColumnDirective field='ShipName' width='170' textAlign="Right"/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

## Diacritics

By default, grid ignores diacritic characters while filtering. To include diacritic characters, set the
[`filterSettings.ignoreAccent`](../api/grid/filter/#ignoreaccent) as **true**.

In the following sample, type **aero** in **Name** column to filter diacritic characters.

{% tab template="grid/filter-diacritics", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids'
import * as React from 'react';
import { diacriticsData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public FilterOptions: FilterSettingsModel = {
    ignoreAccent: true
  };
  public render() {
      return <GridComponent dataSource={diacriticsData} filterSettings={this.FilterOptions} allowFiltering={true}>
          <ColumnsDirective>
              <ColumnDirective field='EmployeeID' width='140' textAlign="Right"/>
              <ColumnDirective field='Name' width='140'/>
              <ColumnDirective field='ShipName' width='170' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='140' textAlign="Right"/>
          </ColumnsDirective>
          <Inject services={[Filter]} />
      </GridComponent>
  }
};
```

{% endtab %}

## See also

* [Customizing Filter Dialog by using an additional parameter](./how-to/add-params-for-filtering)
* [Hide sorting options on Excel filter Dialog](./how-to/hide-sorting-in-excel-filter)
* [How to create a custom menu component to do date range filtering in React Grid](https://www.syncfusion.com/forums/162774/how-to-create-a-custom-menu-component-to-do-date-range-filtering-in-react-grid)
* [How to show the active and outdated records in React Grid](https://www.syncfusion.com/forums/158310/how-to-show-the-active-and-outdated-records-in-react-grid)