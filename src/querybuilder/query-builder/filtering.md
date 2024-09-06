---
title: "Filtering"
component: "QueryBuilder"
description: "Learn how to filtering in the Essential JS 2 QueryBuilder control."
---

# Filtering

Query Builder allows you to create or delete conditions and groups. You can use [`showButtons`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#showbuttons) to enable/disable these buttons.

You can create or delete conditions by interacting through the user interface and methods.

* Use the [`addRules`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#addrules), and [`deleteRules`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#deleterules) methods to create/delete conditions.
* Use [`addGroups`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#addgroups), and [`deleteGroups`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#deletegroups) methods to create/delete groups.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", isDefaultActive=true, compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnsModel, QueryBuilderComponent, RuleModel, ShowButtonsModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;
    public ButtonOptions: ShowButtonsModel = {
        groupDelete: true,
        groupInsert: true,
        ruleDelete: true
    };

    public columnData: ColumnsModel[] = [
        { field: 'EmployeeID', label: 'EmployeeID', type: 'number' },
        { field: 'FirstName', label: 'First Name', type: 'string' },
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

    constructor(props: any) {
        super(props);
        this.addGroup = this.addGroup.bind(this);
        this.addRule = this.addRule.bind(this);
        this.deleteGroup = this.deleteGroup.bind(this);
    }
    public addGroup(): void {
        this.qryBldrObj.addGroups([{'condition': 'and','rules': [{'label': 'First Name','field': 'FirstName','type': 'string','operator': 'startswith','value': 'v' }]}], 'group0');
    }
    public addRule(): void {
        this.qryBldrObj.addRules([{'label': 'City','field': 'City','type': 'string','operator': 'equal','value': 'US'}], 'group0');
    }
    public deleteGroup(): void {
        this.qryBldrObj.deleteGroups(['group1']);
    }

    public render() {
        return (
            <div>
                <QueryBuilderComponent width='100%' dataSource={employeeData} columns={this.columnData}
                rule={this.importRules}  ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }} showButtons={this.ButtonOptions}/>
                <div className="e-qb-button">
                    <ButtonComponent id="addgroup" cssClass='e-primary' content='Add Group' onClick = {this.addGroup}/>
                    <ButtonComponent id="addrules" cssClass='e-primary' content='Add Rule' onClick = {this.addRule}/>
                    <ButtonComponent id="deletegroups" cssClass='e-primary' content='Delete Group' onClick = {this.deleteGroup}/>
                </div>
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}