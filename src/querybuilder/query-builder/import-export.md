---
title: "Importing and Exporting"
component: "QueryBuilder"
description: "Learn how to importing and exporting the rules in the Essential JS 2 QueryBuilder control."
---

# Importing

Importing allows you to view or edit the predefined conditions which is available in JSON or SQL. You can import the conditions either initial rendering or post rendering.

## Initial rendering

To apply conditions initially, you can define the [`rule`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#rule). Here, you can import structured JSON object by defining the [`rule`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#rule) property.

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
            <QueryBuilderComponent width='100%' dataSource={hardwareData} columns={this.columnData}  rule={this.importRules}/>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

## Post rendering

### Importing from JSON

You can set the conditions from structured JSON object through the [`setRules`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#setrules) method.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { hardwareData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;

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
    constructor(props: any) {
        super(props);
        this.onClick = this.onClick.bind(this);
    }
    public onClick(): void {
        this.qryBldrObj.setRules(this.importRules);
    }
    public render() {
        return (
            <div>
                <QueryBuilderComponent width='100%' dataSource={hardwareData}  ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }} columns={this.columnData}/>
                <div className="e-qb-button">
                    <ButtonComponent id="importrules" cssClass='e-primary' content='Set Rules' onClick = {this.onClick}/>
                </div>
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

### Importing from SQL

You can set the conditions from SQL query through the [`setRulesFromSql`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#setrulesfromsql) method.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { QueryBuilderComponent, ColumnsModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { hardwareData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;

    public columnData: ColumnsModel[] = [
        { field: 'TaskID', label: 'Task ID', type: 'number' },
        { field: 'Name', label: 'Name', type: 'string' },
        { field: 'Category', label: 'Category', type: 'string' },
        { field: 'SerialNo', label: 'Serial No', type: 'string' },
        { field: 'InvoiceNo', label: 'Invoice No', type: 'string' },
        { field: 'Status', label: 'Status', type: 'string' }
    ];
    constructor(props: any) {
        super(props);
        this.importRule = this.importRule.bind(this);
    }
    public importRule(): void {
        this.qryBldrObj.setRulesFromSql("TaskID = 1 and Status LIKE ('Assigned%')");
    }
    public render() {
        return (
            <div>
                <QueryBuilderComponent width='100%' dataSource={hardwareData} ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }} columns={this.columnData}/>
                <div className="e-qb-button">
                    <ButtonComponent id="importrules" cssClass='e-primary' content='set Rules' onClick = {this.importRule}/>
                </div>
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

# Exporting

Exporting allows you to save or maintain the created conditions through the Query Builder. You can export the defined conditions by the following ways.

## Exporting to JSON

You can export the defined conditions to structured JSON object through the [`getRules`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#getrules) method.

## Exporting to SQL

You can export the defined conditions to SQL query through the [`getRulesFromSQL`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#getrulesfromsql) method.

{% tab template="query-builder/import-export", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { AnimationSettingsModel, DialogComponent } from '@syncfusion/ej2-react-popups';
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { hardwareData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;
    public dialogInstance: DialogComponent;
    public animationSettings: AnimationSettingsModel = { effect: 'Zoom', duration: 400, delay: 0 };
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
    constructor(props: any) {
        super(props);
        this.getSql = this.getSql.bind(this);
        this.getRule = this.getRule.bind(this);
    }
    public getSql(): void {
        this.dialogInstance.content = this.qryBldrObj.getSqlFromRules(this.qryBldrObj.getRules());
        this.dialogInstance.show();
    }
    public getRule(): void {
        const validRule = this.qryBldrObj.getValidRules(this.qryBldrObj.rule);
        this.dialogInstance.content = '<pre>' + JSON.stringify(validRule, null, 4) + '</pre>';
        this.dialogInstance.show();
    }
    public render() {
        return (
            <div>
                <QueryBuilderComponent width='100%' dataSource={hardwareData} ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }} columns={this.columnData} rule={this.importRules}/>
                <div className="e-qb-button">
                    <ButtonComponent cssClass='e-primary' content='Get Sql' onClick = {this.getSql}/>
                    <ButtonComponent cssClass='e-primary' content='Get Rule' onClick = {this.getRule}/>
                </div>
                <DialogComponent id="defaultdialog" showCloseIcon={true} animationSettings={this.animationSettings} ref={dialog => this.dialogInstance = dialog as DialogComponent} height='auto'  header='Querybuilder' visible={false} width='50%' />
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}