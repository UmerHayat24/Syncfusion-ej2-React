---
title: "State Maintanance in Query Builder"
component: "Query Builder"
description: "This section helps to learn how to maintain the State in React QueryBuilder Component."
---

# Maintain the state persistence

State persistence allows you to maintain the current state in the browser’s `localStorage` even if the browser is refreshed or if you move to the next page within the browser. State persistence stores the Query Builder’s [`rule`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#rule) object in the local storage when the [`enablePersistence`](https://ej2.syncfusion.com/react/documentation/state-persistence/) is defined to true.

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
        }]
    };

    public render() {
        return (
            <QueryBuilderComponent width='100%' enablePersistence={true} dataSource={hardwareData} columns={this.columnData} rule={this.importRules} />
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}