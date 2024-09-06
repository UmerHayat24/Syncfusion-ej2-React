---
title: "Mode Binding"
component: "QueryBuilder"
description: "Documentation on model binding in the Essential JS 2 QueryBuilder control."
---

# Model Binding

Model binding allows to bind properties for the components used in field, operator, and value columns. To implement model binding, assign fieldModel, operatorModel, and valueModel properties in QueryBuilder.

{% tab template="query-builder/model-binding", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { QueryBuilderComponent, ColumnsDirective, ColumnDirective  } from '@syncfusion/ej2-react-querybuilder';
import { RuleModel,  ColumnsModel, ValueModel } from '@syncfusion/ej2-querybuilder';
import { DropDownListModel } from '@syncfusion/ej2-dropdowns';
import * as React from 'react';
import * as ReactDom from 'react-dom';
class App extends React.Component {
        public field: DropDownListModel = {
            allowFiltering : true,
            popupHeight: '400px'
        }
       public operator: DropDownListModel= {
            allowFiltering : true,
            popupHeight: '400px'
        }
        public value: ValueModel = {
            numericTextBoxModel: {
                cssClass: 'e-custom'
            },
            multiSelectModel: {
                cssClass: 'e-custom'
            },
            datePickerModel: {
                cssClass: 'e-custom'
            },
            textBoxModel: {
                cssClass: 'e-custom'
            },
            radioButtonModel: {
                cssClass: 'e-custom'
            }
        }
        public importRules: RuleModel = {
            'condition': 'and',
            'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1001
            }]
        };
    render() {
        return (<div>
            <QueryBuilderComponent width='100%' rule={this.importRules} id='querybuilder' enableNotCondition ="true" fieldModel ={this.field} operatorModel = {this.operator} valueModel = {this.value} >
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
export default App;
ReactDom.render(<App />,document.getElementById('querybuilder-component'));
```

{% endtab %}