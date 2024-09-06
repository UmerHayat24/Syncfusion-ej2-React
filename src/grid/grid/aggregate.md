---
title: "Aggregates"
component: "Grid"
description: "Learn how to aggregate rows, apply custom aggregates, and format the aggregate values in the Essential JS 2 DataGrid control."
---

# Aggregates

Aggregate values are displayed in the footer, group footer, or group caption of the Grid. It can be configured through [`aggregates`](../api/grid/#aggregates) property.
 [`field`](../api/grid/aggregateColumn/#field) and [`type`](../api/grid/aggregateColumn/#type)
 are the minimum properties required to represent an aggregate column.

To use the aggregate feature, you have to inject the **Aggregate** module.

By default, the aggregate value can be displayed in the footer, group, and caption cells. To show the aggregate value in one of the cells, use the [`footerTemplate`](../api/grid/aggregateColumn/#footertemplate), [`groupFooterTemplate`](../api/grid/aggregateColumn/#groupfootertemplate), or [`groupCaptionTemplate`](../api/grid/aggregateColumn/#groupcaptiontemplate) property.

## Built-in aggregate types

The aggregate type should be specified in the [`type`](../api/grid/aggregateColumn/#type) property to configure an aggregate column.

The built-in aggregates are,
* Sum
* Average
* Min
* Max
* Count
* Truecount
* Falsecount

> * Multiple aggregates can be used for an aggregate column by setting the [`type`](../api/grid/aggregateColumn/#type) property
with an array of aggregate types.
> * Multiple types for a column is supported only when one of the aggregate templates is used.

## Footer aggregate

Footer aggregate value is calculated for all the rows, and it is displayed in the footer cells. Use the [`footerTemplate`](../api/grid/aggregateColumn/#footertemplate) property to render the aggregate value in footer cells.

{% tab template="grid/aggregate", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { AggregateColumnDirective, ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import { Aggregate, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public footerSum(props: any) : any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public footerMax(props: any) : any{
    return(<span>Maximum: {props.Max}</span>)
  }
  public render(){
      return <GridComponent  dataSource={data} allowPaging={true} height={268}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='Freight' headerText='Freight' width='150' textAlign='Right'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <AggregatesDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' footerTemplate={this.footerSum} />
                  </AggregateColumnsDirective>
                </AggregateDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Max' footerTemplate={this.footerMax}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
              </AggregatesDirective>
              <Inject services={[Page, Aggregate]}/>
          </GridComponent>
      }
}
```

{% endtab %}

> The aggregate values must be accessed inside the template using their corresponding [`type`](../api/grid/aggregateColumn/#type) name.

## How to format aggregate value

You can format the aggregate value result by using the [`format`](../api/grid/aggregateColumn/#format) property.

{% tab template="grid/aggregate", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { AggregateColumnDirective, ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import { Aggregate, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public footerSum(props: any) : any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public footerMax(props: any) : any{
    return(<span>Maximum: {props.Max}</span>)
  }
  public render(){
      return <GridComponent  dataSource={data} allowPaging={true} height={268}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='Freight' headerText='Freight' format='C2' width='150' textAlign='Right'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <AggregatesDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2' footerTemplate={this.footerSum} />
                  </AggregateColumnsDirective>
                </AggregateDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Max' format='C2' footerTemplate={this.footerMax}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
              </AggregatesDirective>
              <Inject services={[Page, Aggregate]}/>
          </GridComponent>
      }
}
```

{% endtab %}

## Group and caption aggregate

Group and caption aggregate values are calculated from the current group items.
If [`groupFooterTemplate`](../api/grid/aggregateColumn/#groupfootertemplate) is provided, the aggregate values are displayed in the group footer cells; and if [`groupCaptionTemplate`](../api/grid/aggregateColumn/#groupcaptiontemplate)
 is provided, aggregate values are displayed in the group caption cells.

{% tab template="grid/aggregate", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { AggregateColumnDirective, ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import { Aggregate, Group, GroupSettingsModel, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions : GroupSettingsModel = {
    columns: ['ShipCountry'],
    showDropArea: false
  };
  public footerSum(props: any) : any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public footerMax(props: any) : any {
    return(<span>Maximum: {props.Max}</span>)
  }
  public render() {
    return <GridComponent  dataSource={data} allowPaging={true} allowGrouping={true}
              groupSettings={this.groupOptions} height={268}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='OrderDate' headerText='OrderDate' format='yMd' width='150'/>
                <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' width='150'/>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
            </ColumnsDirective>
            <AggregatesDirective>
              <AggregateDirective>
                <AggregateColumnsDirective>
                  <AggregateColumnDirective field='Freight' type='Sum' format='C2' groupFooterTemplate={this.footerSum}/>
                </AggregateColumnsDirective>
              </AggregateDirective>
              <AggregateDirective>
                <AggregateColumnsDirective>
                  <AggregateColumnDirective field='Freight' type='Max' format='C2' groupCaptionTemplate={this.footerMax}/>
                </AggregateColumnsDirective>
              </AggregateDirective>
            </AggregatesDirective>
            <Inject services={[Page, Aggregate, Group]}/>
        </GridComponent>
  }
}
```

{% endtab %}

> The aggregate values must be accessed inside the template using their corresponding [`type`](../api/grid/aggregateColumn/#type)
name.

## Custom aggregate

To calculate the aggregate value with your own aggregate functions, use the custom aggregate option. To use custom aggregation, specify the [`type`](../api/grid/aggregateColumn/#type) as **Custom**, and provide the custom aggregate function in the [`customAggregate`](../api/grid/aggregateColumn/#customaggregate) property.

The custom aggregate function will be invoked with different arguments for total and group aggregations.
* **Total aggregation**: The custom aggregate function will be called with the whole data and current [`AggregateColumn`](../api/grid/aggregateColumn/)
object.
* **Group aggregation**: This will be called with the current group details and [`AggregateColumn`](../api/grid/aggregateColumn/) object.

{% tab template="grid/aggregate", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { AggregateColumnDirective, ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import { Aggregate, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public custom(props: any): any {
    return(<span>Custom: {props.Custom}</span>)
  }
  public customAggregateFn(args: any, aggColumn: any): any{
      const val = args.result.filter((item: any) => item[aggColumn.columnName] === 'Brazil').length;
      return val;
  };
  public render() {
    return <GridComponent  dataSource={data} allowPaging={true} height={240}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='Freight' headerText='Freight' format='C2' width='150'/>
                <ColumnDirective field='ShipCountry' headerText='Ship Name' width='150'/>
            </ColumnsDirective>
            <AggregatesDirective>
              <AggregateDirective>
                <AggregateColumnsDirective>
                  <AggregateColumnDirective field='ShipCountry' type='Custom'
                    customAggregate ={this.customAggregateFn} footerTemplate={this.custom} />
                </AggregateColumnsDirective>
              </AggregateDirective>
            </AggregatesDirective>
            <Inject services={[Page, Aggregate]}/>
        </GridComponent>
  }
}
```

{% endtab %}

> To access the custom aggregate value inside the template, use the key as **Custom**.

## Reactive aggregate update

When using batch editing, the aggregate values will be refreshed on every cell save. The footer, group footer, and group caption aggregate values will be refreshed.

> Adding a new record to the grouped grid will not refresh the aggregate values.

{% tab template="grid/aggregate", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { AggregateColumnDirective, ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import { Aggregate, Edit, Group, Page, PageSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public pageSettings: PageSettingsModel = { pageSize: 7 };
  public toolbarOptions: ToolbarItems[] = ['Delete', 'Update', 'Cancel'];
  public editOption = { allowEditing: true, allowDeleting: true, mode: 'Batch' };
  public groupOptions = { columns: ['ShipCountry'] }
  public footerSum(props: any): any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public groupFooterSum(props: any): any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public footerAvg(props: any): any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public render(){
    return <GridComponent dataSource={data} allowPaging={true} pageSettings={this.pageSettings}
              allowGrouping={true} groupSettings={this.groupOptions}
              toolbar= {this.toolbarOptions} editSettings={this.editOption} height={268}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' isPrimaryKey={true} width='120' textAlign='Right'/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='Freight'  headerText='Freight' format='C2' editType= 'numericedit' textAlign='Right' width='150'/>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
              </ColumnsDirective>
              <AggregatesDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2'
                    footerTemplate={this.footerSum}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2'
                    groupFooterTemplate={this.groupFooterSum}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2'
                    groupCaptionTemplate={this.footerAvg}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
              </AggregatesDirective>
            <Inject services={[Page, Aggregate, Edit, Group]}/>
        </GridComponent>
      }
}
```

{% endtab %}

### Refresh aggregates in inline edit mode

By default, reactive aggregate update is not supported by inline and dialog edit modes as it is not feasible to anticipate the value change event for every editor. But, you can refresh the aggregates manually in the inline edit mode using the refresh method of aggregate module.

In the following code, the input event for the Freight column editor has been registered and the aggregate value has been refreshed manually.

{% tab template="grid/aggregate", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { setValue } from '@syncfusion/ej2-base';
import { AggregateColumnDirective, ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateDirective, AggregatesDirective, Grid } from '@syncfusion/ej2-react-grids';
import { Aggregate, Edit, EditEventArgs, Group, Page, PageSettingsModel, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public numericParams = {params:{change: this.changeFn.bind(this)}}
  public pageSettings: PageSettingsModel = { pageSize: 7 };
  public toolbarOptions: ToolbarItems[] = ['Delete', 'Update', 'Cancel'];
  public editOption = { allowEditing: true, allowDeleting: true, mode: 'Normal' };
  public groupOptions = { columns: ['ShipCountry'] };
  public selectedRecord: object = {};
  public actionBegin(args: EditEventArgs){
   if(args.requestType === 'beginEdit'){
         this.selectedRecord ={};
         this.selectedRecord = args.rowData as object;
      };
  }
  public changeFn(args: any){
    setValue('Freight', args.value, this.selectedRecord);
    if (this.grid) {
      this.grid.aggregateModule.refresh(this.selectedRecord);
    }
  }
  public footerSum(props: any): any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public groupFooterSum(props: any): any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public footerAvg(props: any): any {
    return(<span>Sum: {props.Sum}</span>)
  }
  public render(){
    this.actionBegin = this.actionBegin.bind(this);
    return <GridComponent dataSource={data} ref={g => this.grid = g} allowPaging={true} pageSettings={this.pageSettings}
              allowGrouping={true} groupSettings={this.groupOptions} actionBegin={this.actionBegin}
              toolbar= {this.toolbarOptions} editSettings={this.editOption} height={268}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' isPrimaryKey={true} width='120' textAlign='Right'/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='Freight'  headerText='Freight' format='C2' edit={this.numericParams} editType= 'numericedit' textAlign='Right' width='150'/>
                <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
              </ColumnsDirective>
              <AggregatesDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2'
                    footerTemplate={this.footerSum}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2'
                    groupFooterTemplate={this.groupFooterSum}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
                <AggregateDirective>
                  <AggregateColumnsDirective>
                    <AggregateColumnDirective field='Freight' type='Sum' format='C2'
                    groupCaptionTemplate={this.footerAvg}/>
                  </AggregateColumnsDirective>
                </AggregateDirective>
              </AggregatesDirective>
            <Inject services={[Page, Aggregate, Edit, Group]}/>
        </GridComponent>
      }
}
```

{% endtab %}
