---
title: "Sort the columns in Query Builder"
component: "Query Builder"
description: "This section helps to learn how to sort columns in React QueryBuilder Component."
---

# Sort the columns

SortDirection allows you to sort the columns bounded to the Query Builder to view the columns by ascending or descending order. You should set the [`sortDirection`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#sortdirection) property to sort the fields.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", isDefaultActive=true, compileJsx=true %}

```tsx
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { hardwareData } from '../datasource.ts';

class App extends React.Component<{}, {}> {

    public columnData: ColumnsModel[] = [
        { field: 'TaskID', label: 'Task ID', type: 'number' },
        { field: 'Name', label: 'Name', type: 'string' },
        { field: 'Category', label: 'Category', type: 'string' },
        { field: 'SerialNo', label: 'Serial No', type: 'string' },
        { field: 'InvoiceNo', label: 'Invoice No', type: 'string' },
        { field: 'Status', label: 'Status', type: 'string' }
    ];
    public importRules: RuleModel = {
        'condition': 'or',
        'rules': [{
            'field': 'Category',
            'label': 'Category',
            'operator': 'equal',
            'type': 'string',
            'value': 'Laptop'
        },
        {
        'condition': 'and',
            'rules': [{
                'field': 'Status',
                'label': 'Status',
                'operator': 'notequal',
                'type': 'string',
                'value': 'Pending'
            },
            {
                'field': 'TaskID',
                'label': 'Task ID',
                'operator': 'equal',
                'type': 'number',
                'value': 5675
            }]
        }]
    };

    public render() {
        return (
            <QueryBuilderComponent width='100%' sortDirection="Ascending" dataSource={hardwareData} columns={this.columnData} rule={this.importRules} />
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}