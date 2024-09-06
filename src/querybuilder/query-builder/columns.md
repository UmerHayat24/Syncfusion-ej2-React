---
title: "Columns"
component: "QueryBuilder"
description: "Documentation on column  step, format in the Essential JS 2 QueryBuilder control."
---

# Columns

The column definitions are used as the [`dataSource`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#datasource) schema in the Query Builder. This plays a vital role in rendering column values. The query builder operations such as create or delete conditions and create or delete group they are performed based on the column definitions. The [`field`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#field) property of the columns is necessary to map the data source values in the query builder columns.

> If the column field is not specified in the [`dataSource`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#datasource), the column values will be empty.

## Auto generation

The [`columns`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#columns) are automatically generated when the [`columns`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#columns) declaration is empty or undefined while initializing the query builder. All the columns in the [`dataSource`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#datasource) are bound as the query builder columns.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts, isDefaultActive=true", compileJsx=true %}

```tsx
import { QueryBuilderComponent } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public render() {
        return (
            <QueryBuilderComponent width='100%' dataSource={employeeData}/>
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

> When columns are auto-generated, the column type will be determined from the first record of the [`dataSource`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#datasource).

## Labels

By default, the column label is displayed from the column [`field`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#field) value. To override the default label, you have to define the [`label`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#label) value.

## Operators

The operator for a column can be defined in the [`operators`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#operators) property.
The available operators and its supported data types are:

| Operators | Description | Supported Types |
| ------------ | ----------------------- | ------------------ |
| startswith  | Checks whether the value begins with the specified value. | String |
| endswith  | Checks whether the value ends with the specified value. | String |
| contains | Checks whether the value contains the specified value. | String |
| equal | Checks whether the value is equal to the specified value. | String Number Date Boolean |
| notequal | Checks whether the value is not equal to the specified value. | String Number Date Boolean |
| greaterthan | Checks whether the value is greater than the specified value. | Date Number |
| greaterthanorequal | Checks whether a value is greater than or equal to the specified value. | Date Number |
| lessthan | Checks whether the value is less than the specified value.| Date Number |
| lessthanorequal | Checks whether the value is less than or equal to the specified value. | Date Number |
| between | Checks whether the value is between the two-specific value. | Date  Number |
| notbetween | Checks whether the value is not between the two-specific value. | Date  Number |
| in | Checks whether the value is one of the specific values. | String  Number |
| notin | Checks whether the value is not in the specific values. | String  Number |

## Step

The Query Builder allows you to set the step values to the number fields. So that you can easily access the numeric textbox. Use the [`step`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#step) property, to set the step value for number values.

## Format

The Query Builder formats date and number values. Use the [`format`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#format) property to format date and number values.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}> {

    public columnData: ColumnsModel[] = [
        { field: 'EmployeeID', label: 'Employee ID', operators: [{ key: 'Equal', value: 'equal' },
            { key: 'Greater than', value: 'greaterthan' }, { key: 'Less than', value: 'lessthan' }],  step: 10, type: 'number'},
        { field: 'FirstName', label: 'First Name', type: 'string' },
        { field: 'TitleOfCourtesy', label: 'Title Of Courtesy', type: 'boolean', values: ['Mr.', 'Mrs.'] },
        { field: 'Title', label: 'Title', type: 'string' },
        { field: 'HireDate', label: 'Hire Date', type: 'date', format: 'dd/MM/yyyy' },
        { field: 'Country', label: 'Country', type: 'string' },
        { field: 'City', label: 'City', type: 'string' }
    ];
    public importRules: RuleModel = {
        'condition': 'and',
        'rules': [{
            'field': 'EmployeeID',
            'label': 'Employee ID',
            'operator': 'equal',
            'type': 'number',
            'value': 1001
        },
        {
            'field': 'HireDate',
            'label': 'Hire Date',
            'operator': 'equal',
            'type': 'date',
            'value': '07/05/1991'
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
            <QueryBuilderComponent width='100%' dataSource={employeeData} columns={this.columnData}
            rule={this.importRules} />
        );
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

## Validations

Validation allows you to validate the conditions and it display errors for invalid fields while using  the [`validateFields`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#validatefields) method.  To enable validation in the query builder , set the allowValidation to true. Column fields are validated after setting [`allowValidation`](https://ej2.syncfusion.com/react/documentation/api/query-builder/#allowvalidation) as to true. So, you should manually configure the validation for Operator and, Value fields through [`validation`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#validation).

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnsModel, QueryBuilderComponent } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { employeeData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;

    public columnData: ColumnsModel[] = [
        { field: 'EmployeeID', label: 'EmployeeID', type: 'number', validation: { isRequired: true } },
        { field: 'FirstName', label: 'FirstName', type: 'string' },
        { field: 'TitleOfCourtesy', label: 'Title Of Courtesy', type: 'boolean', values: ['Mr.', 'Mrs.'] },
        { field: 'Title', label: 'Title', type: 'string' },
        { field: 'HireDate', format: 'dd/MM/yyyy', label: 'HireDate', type: 'date' },
        { field: 'Country', label: 'Country', type: 'string' },
        { field: 'City', label: 'City', type: 'string' }
    ];
    constructor(props: any) {
        super(props);
        this.onClick = this.onClick.bind(this);
    }
    public onClick(): void {
        this.qryBldrObj.validateFields();
    }

    public render() {
        return (
            <div>
                <QueryBuilderComponent width='100%' dataSource={employeeData} columns={this.columnData} allowValidation={true} ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }}/>
                <div className="e-qb-button">
                    <ButtonComponent id="validatebtn" cssClass='e-primary' content='Validate Fields' onClick = {this.onClick} />
                </div>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

> Set [`isRequired`](https://ej2.syncfusion.com/react/documentation/api/query-builder/validation/#isrequired) validation for Operator and Value fields.
> Set [`min`](https://ej2.syncfusion.com/react/documentation/api/query-builder/validation/#min), [`max`](https://ej2.syncfusion.com/react/documentation/api/query-builder/validation/#max) values for number values.