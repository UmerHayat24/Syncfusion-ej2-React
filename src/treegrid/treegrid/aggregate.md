---
title: "Aggregates"
component: "TreeGrid"
description: "Learn how to aggregate rows, apply custom aggregates, and format the aggregate values in the Essential JS 2 TreeGrid control."
---

# Aggregates

Aggregate values are displayed in the TreeGrid footer and in parent row footer for child row aggregate values. It can be configured through [`aggregates`](../api/treegrid/#aggregates) property. [`field`](../api/treegrid/aggregateColumnModel/#field) and [`type`](../api/treegrid/aggregateColumnModel/#type) are the minimum properties required to represent an aggregate column.

To use the aggregate feature, you have to inject the **Aggregate** module.

By default, the aggregate value can be displayed in the treegrid footer, and footer of child rows. To show the aggregate value in one of the cells, use the [`footerTemplate`](../api/treegrid/aggregateColumnModel/#footertemplate).

To get start quickly with aggregates functionalities, you can check on this video:
`youtube:4Fs8mKL3DCg`

## Built-in aggregate types

The aggregate type should be specified in the [`type`](../api/treegrid/aggregateColumnModel/#type) property to configure an aggregate column.

The built-in aggregates are,
* Sum
* Average
* Min
* Max
* Count
* Truecount
* Falsecount

> * Multiple aggregates can be used for an aggregate column by setting the [`type`](../api/treegrid/aggregateColumnModel/#type) property
with an array of aggregate types.
> * Multiple types for a column is supported only when one of the aggregate templates is used.

## Footer aggregate

Footer aggregate value is calculated for all the rows, and it is displayed in the footer cells. Use the [`footerTemplate`](../api/treegrid/aggregateColumnModel/#footertemplate) property to render the aggregate value in footer cells.

{% tab template="treegrid/aggregate", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject } from '@syncfusion/ej2-grids';
import { Aggregate, AggregatesDirective, ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { AggregateColumnDirective, AggregateColumnsDirective, AggregateDirective, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { summaryRowData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public footerSum(props: object):any{
        return(<span>Minimum: {getObject('Min', props)}</span>)
    }

    public footerSum2(props: object):any{
        return(<span>Maximum: {getObject('Max', props)}</span>)
    }

    public render() {
        return <TreeGridComponent dataSource={summaryRowData} treeColumnIndex={0} childMapping='children' height='260'>
            <ColumnsDirective>
                <ColumnDirective field='FreightID' headerText='Freight ID' width='130'/>
                <ColumnDirective field='FreightName' headerText='Freight Name' width='180'/>
                <ColumnDirective field='UnitWeight' headerText='Weight Per Unit' width='130' textAlign='Right' type='number' />
                <ColumnDirective field='TotalUnits' headerText='Total Units' type='number' width='125' textAlign='Right' />
            </ColumnsDirective>
                <AggregatesDirective>
                <AggregateDirective showChildSummary={false}>
                    <AggregateColumnsDirective>
                    <AggregateColumnDirective field='TotalUnits' columnName='TotalUnits' type='Min'
                        footerTemplate={this.footerSum}/>
                    <AggregateColumnDirective field='UnitWeight' columnName='UnitWeight' type='Max'
                        footerTemplate={this.footerSum2}/>
                    </AggregateColumnsDirective>
                    </AggregateDirective>
            </AggregatesDirective>
            <Inject services={[Aggregate]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> The aggregate values must be accessed inside the template using their corresponding [`type`](../api/treegrid/aggregateColumnModel/#type) name.

## Child aggregate

Aggregate value is calculated for child rows, and it is displayed in the parent row footer. Use the [`showChildSummary`](../api/treegrid/aggregateRowModel/#showchildsummary) property to render the child rows aggregate value.

{% tab template="treegrid/aggregate", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject } from '@syncfusion/ej2-grids';
import { Aggregate, AggregatesDirective, ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { AggregateColumnDirective, AggregateColumnsDirective, AggregateDirective, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { summaryRowData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public footerSum(props: object):any {
        return(<span>Minimum: {getObject('Min', props)}</span>)
    }

    public footerSum2(props: object):any {
        return(<span>Maximum: {getObject('Max', props)}</span>)
    }

    public render() {
        return <TreeGridComponent dataSource={summaryRowData} treeColumnIndex={0} childMapping='children' height='260'>
            <ColumnsDirective>
                <ColumnDirective field='FreightID' headerText='Freight ID' width='90' textAlign='Right'/>
                <ColumnDirective field='FreightName' headerText='Freight Name' width='195'/>
                <ColumnDirective field='UnitWeight' headerText='Weight Per Unit' width='130' textAlign='Right' type='number' />
                <ColumnDirective field='TotalUnits' headerText='Total Units' type='number' width='125' textAlign='Right' />
            </ColumnsDirective>
                <AggregatesDirective>
                    <AggregateDirective showChildSummary={true}>
                        <AggregateColumnsDirective>
                            <AggregateColumnDirective field='TotalUnits' columnName='TotalUnits' type='Min'
                                footerTemplate={this.footerSum}/>
                            <AggregateColumnDirective field='UnitWeight' columnName='UnitWeight' type='Max'
                                footerTemplate={this.footerSum2}/>
                        </AggregateColumnsDirective>
                    </AggregateDirective>
                </AggregatesDirective>
            <Inject services={[Aggregate]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## How to format aggregate value

You can format the aggregate value result by using the [`format`](../api/treegrid/aggregateColumnModel/#format) property.

{% tab template="treegrid/aggregate", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject } from '@syncfusion/ej2-grids';
import { Aggregate, AggregatesDirective, ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { AggregateColumnDirective, AggregateColumnsDirective, AggregateDirective, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { summaryData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public footerSum(props: object):any{
        return(<span>Total: {getObject('Sum', props)}</span>)
      }

    public render() {
        return <TreeGridComponent dataSource={summaryData} treeColumnIndex={0} childMapping='subtasks' height='260'>
            <ColumnsDirective>
                <ColumnDirective field='category' headerText='Category' width='160'/>
                <ColumnDirective field='units' headerText='Total Units' width='130' type='number' textAlign='Right'/>
                <ColumnDirective field='unitPrice' headerText='Unit Price($)' width='110' textAlign='Right' type='number' format='C2' />
                <ColumnDirective field='price' headerText='Price($)' type='number' width='160' textAlign='Right' format='C2' />
            </ColumnsDirective>
                <AggregatesDirective>
                <AggregateDirective showChildSummary={true}>
                    <AggregateColumnsDirective>
                    <AggregateColumnDirective field='price' columnName='price' type='Sum'
                        footerTemplate={this.footerSum} format='C2'/>
                    </AggregateColumnsDirective>
                    </AggregateDirective>
            </AggregatesDirective>
            <Inject services={[Aggregate]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Custom aggregate

To calculate the aggregate value with your own aggregate functions, use the custom aggregate option. To use custom aggregation, specify the [`type`](../api/treegrid/aggregateColumnModel/#type) as **Custom**, and provide the custom aggregate function in the [`customAggregate`](../api/treegrid/aggregateColumnModel/#customaggregate) property.

{% tab template="treegrid/aggregate", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject } from '@syncfusion/ej2-grids';
import { Aggregate, AggregatesDirective, ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { AggregateColumnDirective, AggregateColumnsDirective, AggregateDirective, Inject } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { summaryData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public footerSum(props: object): any {
        return(<span>Total: {getObject('Sum', props)}</span>)
    }

    public customAggregateFn(row: object): any {
        const sampleData: object[] = getObject('result', row);
        let countLength: number = 0;
        sampleData.filter((item: object) => {
            const data: string = getObject('category', item);
            const value: string = 'Frozen seafood';
            if (data === value) {
                countLength++;
            }
        });
        return countLength;
    }

    public custom(props: object):any{
        return(<span> Count of Frozen seafood: {getObject('Custom', props)}</span>)
    }

    public render() {
        return <TreeGridComponent dataSource={summaryData} treeColumnIndex={0} childMapping='subtasks' height='260'>
            <ColumnsDirective>
                <ColumnDirective field='category' headerText='Category' width='160'/>
                <ColumnDirective field='units' headerText='Total Units' width='130' type='number' textAlign='Right'/>
                <ColumnDirective field='unitPrice' headerText='Unit Price($)' width='90' textAlign='Right' type='number' format='C2' />
                <ColumnDirective field='price' headerText='Price($)' type='number' width='160' textAlign='Right' format='C' />
            </ColumnsDirective>
                <AggregatesDirective>
                <AggregateDirective showChildSummary={false}>
                    <AggregateColumnsDirective>
                    <AggregateColumnDirective field='price' columnName='category' type='Custom'
                        customAggregate ={this.customAggregateFn} footerTemplate={this.custom}/>
                    </AggregateColumnsDirective>
                    </AggregateDirective>
            </AggregatesDirective>
            <Inject services={[Aggregate]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> To access the custom aggregate value inside the template, use the key as **Custom**.
