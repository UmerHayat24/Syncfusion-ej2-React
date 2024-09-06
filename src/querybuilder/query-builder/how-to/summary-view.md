---
title: "How To"
component: "QueryBuilder"
description: "This section helps to learn how to create the query builder in React application with its basic features in step-by-step procedure."
---

# Summary View

Summary view allows you to show or hide the filtered query. By default, the value is false. You can enable by setting the [`summaryView`](https://ej2.syncfusion.com/documentation/api/query-builder/#summaryview) property to true.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { QueryBuilderComponent, ColumnsModel, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import { employeeData } from '../datasource.ts';


export default class App extends React.Component<{}, {}> {

    columnData: ColumnsModel[] = [
        { field: 'EmployeeID', label: 'EmployeeID', type: 'number'},
        { field: 'FirstName', label: 'FirstName', type: 'string' },
        { field: 'TitleOfCourtesy', label: 'Title Of Courtesy', type: 'boolean', values: ['Mr.', 'Mrs.'] },
        { field: 'Title', label: 'Title', type: 'string' },
        { field: 'HireDate', label: 'HireDate', type: 'date', format: 'dd/MM/yyyy' },
        { field: 'Country', label: 'Country', type: 'string' },
        { field: 'City', label: 'City', type: 'string' }
    ];
    importRules: RuleModel = {
        'condition': 'and',
        'rules': [{
        'label': 'EmployeeID',
        'field': 'EmployeeID',
        'type': 'number',
        'operator': 'notequal',
        'value': '5'
    },
    {
        'condition': 'or',
        'rules': [{
        'label': 'Title Of Courtesy',
        'field': 'TitleOfCourtesy',
        'type': 'string',
        'operator': 'equal',
        'value': 'Mr.'
        },
        {
        'label': 'Country',
        'field': 'Country',
        'type': 'string',
        'operator': 'equal',
        'value': 'USA'
        },
        {
        'condition': 'and',
        'rules': [{
        'label': 'City',
        'field': 'City',
        'type': 'string',
        'operator': 'equal',
        'value': 'London'
            }]
        }]
    }]
}

    render() {
        return (
                <QueryBuilderComponent width='30%' dataSource={employeeData} columns={this.columnData} rule={this.importRules} summaryView="true" ></QueryBuilderComponent>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}