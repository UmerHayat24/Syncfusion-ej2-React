---
title: "Display Mode options in Query Builder "
component: "Query Builder"
description: "This section helps to learn how to change the Display Mode"
---

# Change display mode

Display options allow you to view the Query Builder in Vertically or Horizontally. For this, you should use the [`displayMode`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#displaymode) property.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts",iframeHeight="600px", isDefaultActive=true, compileJsx=true %}

```tsx

import { QueryBuilderComponent, ColumnsModel, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}> {

    public columnData:ColumnsModel[] = [
        { field: 'EmployeeID', label: 'EmployeeID', type: 'number' },
        { field: 'FirstName', label: 'FirstName', type: 'string' },
        { field: 'TitleOfCourtesy', label: 'Title Of Courtesy', type: 'boolean', values: ['Mr.', 'Mrs.'] },
        { field: 'Title', label: 'Title', type: 'string' },
        { field: 'HireDate', label: 'HireDate', type: 'date', format: 'dd/MM/yyyy' },
        { field: 'Country', label: 'Country', type: 'string' },
        { field: 'City', label: 'City', type: 'string' }
    ];
    public importRules: RuleModel = {
        'condition': 'and',
        'rules': [{
            'field': 'EmployeeID',
            'label': 'EmployeeID',
            'operator': 'equal',
            'type': 'number',
            'value': 1001
        },
        {
            'field': 'Title',
            'label': 'Title',
            'operator': 'equal',
            'type': 'string',
            'value': 'Sales Manager'
        }]
    };

    public render() {
        return (
            <QueryBuilderComponent width='30%' dataSource={employeeData} columns={this.columnData} rule={this.importRules} displayMode='Vertical' />
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

> The default view the query builder component is Horizontal.
> The default view the query builder component in Vertical.