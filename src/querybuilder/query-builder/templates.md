---
title: "Templates"
component: "QueryBuilder"
description: "Documentation on Templates in the Essential JS 2 QueryBuilder control."
---

# Templates

Templates allows users to define customized header and own user interface for columns.

## Header Template

Header Template allows to define your own user interface for Header, which includes creating or deleting rules and groups and to customize the AND/OR condition and NOT condition options. To implement header template, you can create the user interface as `React` component and assign the values when requestType is header-template-create in `actionBegin` event.

In the following sample dropdown, splitbutton and button are used as the custom components in the header.
{% tab template="query-builder/header-template", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { QueryBuilderComponent, ColumnsDirective, ColumnDirective  } from '@syncfusion/ej2-react-querybuilder';
import { RuleModel } from '@syncfusion/ej2-querybuider';
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { HeaderTemplate } from './template';

class App extends React.Component {
    public qryBldrObj: QueryBuilderComponent;
    public importRules: RuleModel = {
            'condition': 'and', 'not': true,
            'rules': [{
                    'field': 'Age',
                    'label': 'Age',
                    'operator': 'equal',
                    'type': 'number',
                    'value': 30
                },
                {
                    'label': 'LastName',
                    'field': 'LastName',
                    'type': 'string',
                    'operator': 'equal',
                    'value': 'vinit'
                },
                {
                    'condition': 'or',
                    'rules': [{
                      'label': 'Age',
                      'field': 'Age',
                      'type': 'number',
                      'operator': 'equal',
                      'value': 34
                    }]
                }
            ]
        };
    public headerTemplate(props): any {
        return (<HeaderTemplate {...props}/>);
    }
    public render() {
        return (<div>
            <QueryBuilderComponent width='100%' rule={this.importRules} headerTemplate= {this.headerTemplate} id='querybuilder' enableNotCondition ="true" >
                <ColumnsDirective>
                    <ColumnDirective field="EmployeeID" label="Employee ID" type="number"/>
                    <ColumnDirective field="LastName" label="Last Name" type="string"/>
                    <ColumnDirective field="FirstName" label="First Name" type="string"/>
                    <ColumnDirective field="Age" label="Age" type="number"/>
                    <ColumnDirective field="City" label="City" type="string"/>
                    <ColumnDirective field="Country" label="Country" type="string"/>
                </ColumnsDirective>
            </QueryBuilderComponent>
        </div>);
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder-component'));
```

{% endtab %}

## Column Template

Template allows you to define your own input widgets for columns. To implement [`template`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#template), you can define the following functions

* `create`: Creates the custom component.
* `write`: Wire events for the custom component.
* `Destroy`: Destroy the custom component.

In the following sample, dropdown is used as the custom component in the PaymentMode column.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx

import { getComponent } from '@syncfusion/ej2-base';
import { ChangeEventArgs, DropDownList, MultiSelect, MultiSelectChangeEventArgs } from '@syncfusion/ej2-react-dropdowns';
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { expenseData } from '../datasource.ts';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;
    public elem: HTMLElement;
    public dropDownObj: DropDownList;
    public multiSelectObj: MultiSelect;
    public inOperators: string [] = ['in', 'notin'];
    public filter: ColumnsModel[] = [
         {
            field: 'PaymentMode', label: 'Payment Mode', operators: [
                { key: 'Equal', value: 'equal' },
                { key: 'Not Equal', value: 'notequal' },
                { key: 'In', value: 'in' },
                { key: 'Not In', value: 'notin' }
            ], template: {
                create: () => {
                    this.elem = document.createElement('input');
                    this.elem.setAttribute('type', 'text');
                    return this.elem;
                },
                destroy: (args: { elementId: string }) => {
                    this.multiSelectObj = getComponent(document.getElementById(args.elementId) as HTMLElement, 'multiselect') as MultiSelect;
                    if (this.multiSelectObj) {
                        this.multiSelectObj.destroy();
                    }
                    this.dropDownObj = getComponent(document.getElementById(args.elementId) as HTMLElement, 'dropdownlist') as DropDownList;
                    if (this.dropDownObj) {
                        this.dropDownObj.destroy();
                    }
                },
                write: (args: { elements: Element, values: string[] | string, operator: string }) => {
                    const ds = ['Cash', 'Debit Card', 'Credit Card', 'Net Banking', 'Wallet'];
                    if (this.inOperators.indexOf(args.operator) > -1) {
                        this.multiSelectObj = new MultiSelect({
                            change: (e: MultiSelectChangeEventArgs) => {
                                this.qryBldrObj.notifyChange(e.value as string[], e.element);
                            },
                            dataSource: ds,
                            mode: 'CheckBox',
                            placeholder: 'Select Transaction',
                            value: args.values as string []
                        });
                        this.multiSelectObj.appendTo('#' + args.elements.id);
                    } else {
                        this.dropDownObj = new DropDownList({
                            change: (e: ChangeEventArgs) => {
                                this.qryBldrObj.notifyChange(e.itemData.value as string, e.element);
                            },
                            dataSource: ds,
                            value: args.values ? args.values as string : ds[0]
                        });
                        this.dropDownObj.appendTo('#' + args.elements.id);
                    }
                }
            }, type: 'string'
        },
        { field: 'Description', label: 'Description', type: 'string' },
        { field: 'Date', label: 'Date', type: 'date' }
    ];

    public importRules: RuleModel = {
            'condition': 'or',
            'rules': [{
                'field': 'PaymentMode',
                'label': 'PaymentMode',
                'operator': 'equal',
                'type': 'string',
                'value': 'Cash'
            }]
    };

    public render() {
        return (
            <QueryBuilderComponent dataSource={expenseData} columns={this.filter} width='100%' rule={this.importRules} ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }} />
        );
    }
}

ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}

### Using Template

Template allows you to define your own input widgets for columns. To implement template, you can create the user interface as `React` component.

{% tab template="query-builder/template", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { QueryBuilderComponent, ColumnsDirective, ColumnDirective  } from '@syncfusion/ej2-react-querybuilder';
import { RuleModel } from '@syncfusion/ej2-querybuider';
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { PaymentTemplate } from './payment-temp';
import { TransactionTemplate } from './transaction-temp';

class App extends React.Component {
    public qryBldrObj: QueryBuilderComponent;
    public importRules: RuleModel = {
             'condition': 'and',
            'rules': [{
                'label': 'Transaction Type',
                'field': 'TransactionType',
                'type': 'string',
                'operator': 'equal',
                'value': 'Expense'
            },
            {
                'label': 'Payment Mode',
                'field': 'PaymentMode',
                'type': 'string',
                'operator': 'equal',
                'value': 'Cash'
            }]
    };
    public paymentTemplate(props): any {
        return (<PaymentTemplate {...props}/>);
    }
    public transactionTemplate(props): any {
        return (<TransactionTemplate {...props}/>);
    }
    public render() {
        return (<div>
            <QueryBuilderComponent width='100%' rule={this.importRules}  id='querybuilder'  >
                <ColumnsDirective>
                    <ColumnDirective field="Category" label="Category" type="string"/>
                    <ColumnDirective field="PaymentMode" label="PaymentMode" type="string" operators ={this.customOperators} template = {this.paymentTemplate}/>
                    <ColumnDirective field="TransactionType" label="TransactionType" type="string" operators ={this.customOperators} template = {this.transactionTemplate}/>
                    <ColumnDirective field="Description" label="Description" type="string"/>
                    <ColumnDirective field="Date" label="Date" type="string"/>
                    <ColumnDirective field="Amount" label="Amount" type="string"/>
                </ColumnsDirective>
            </QueryBuilderComponent>
        </div>);
    }
}
ReactDom.render(<App />,document.getElementById('querybuilder-component'));
```

{% endtab %}

## Rule Template

Rule Template allows to define your own user interface for columns. To implement [`ruleTemplate`](https://ej2.syncfusion.com/react/documentation/api/query-builder/columnsModel/#ruletemplate), you can create the user interface as `React` component and assign the values through `actionBegin` event.

In the following sample, dropdown and slider are used as the custom component and applied `greaterthanorequal` operator to `Age` column.

{% tab template="query-builder/rule-template", sourceFiles="app/**/*.tsx,index.html,datasource.ts", compileJsx=true %}

```tsx

import { getComponent, setValue } from '@syncfusion/ej2-base';
import { ChangeEventArgs, DropDownList } from '@syncfusion/ej2-react-dropdowns';
import { QueryBuilderComponent, ColumnsDirective, ColumnDirective, RuleModel, ActionEventArgs } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { employeeData } from '../datasource.ts';
import { AgeTemplate } from './template';

class App extends React.Component<{}, {}> {
    public qryBldrObj: QueryBuilderComponent;
    public elem: HTMLElement;

    public importRules: RuleModel = {
            'condition': 'or',
            'rules': [{
                'field': 'Age',
                'label': 'Age',
                'operator': 'greaterthanorequal',
                'type': 'number',
                'value': 30
            }]
    };

    public ageTemplate(props): any {
      return (<AgeTemplate {...props} />);
    }

    public actionBegin(args: ActionEventArgs): void {
      this.ruleID = args.ruleID;
      args.rule.operator = 'greaterthanorequal';
      if (args.requestType === 'template-initialize') {
        if (args.rule.value === '') {
          args.rule.value = 30;
        }
      }
    }

    public render() {
        return (
            <QueryBuilderComponent dataSource={employeeData} width='100%' rule={this.importRules} ref={(scope) => { this.qryBldrObj = scope as QueryBuilderComponent; }} actionBegin={this.actionBegin.bind(this)} id='querybuilder'>
                <ColumnsDirective>
                    <ColumnDirective field="EmployeeID" label="Employee ID" type="number"/>
                    <ColumnDirective field="LastName" label="Last Name" type="string"/>
                    <ColumnDirective field="FirstName" label="First Name" type="string"/>
                    <ColumnDirective field="Age" label="Age" type="number" ruleTemplate={this.ageTemplate}/>
                    <ColumnDirective field="City" label="City" type="string"/>
                    <ColumnDirective field="Country" label="Country" type="string"/>
                </ColumnsDirective>
            </QueryBuilderComponent>
        );
    }
}

ReactDom.render(<App />,document.getElementById('querybuilder-component'));
```

{% endtab %}