---
title: "Localization"
component: "QueryBuilder"
description: "Learn how to Localization library allows you to localize default text content in the Essential JS 2 QueryBuilder control."
---

# Localization

The `Localization` library allows you to localize default text content of the Query Builder. The Query Builder component has static text that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the locale value and translation object.

The following list of properties and its values are used in the Query Builder.

| Locale key words | Text |
| ------------ | ----------------------- |
| AddGroup  | Add Group |
| AddCondition  | Add Condition |
| DeleteRule | Remove this condition |
| DeleteGroup | Delete group |
| Edit | EDIT |
| SelectField | Select a field |
| SelectOperator | Select operator |
| StartsWith | Starts With|
| EndsWith | Ends With |
| Contains | Contains |
| Equal | Equal |
| NotEqual | Not Equal |
| LessThan | Less Than |
| LessThanOrEqual | Less Than Or Equal |
| GreaterThan | Greater Than |
| GreaterThanOrEqual | Greater Than Or Equal |
| Between | Between |
| NotBetween | Not Between|
| In | In |
| NotIn | Not In |
| Remove | REMOVE |
| ValidationMessage | This field is required |
| SummaryViewTitle | Summary View |
| OtherFields | Other Fields |
| AND | AND |
| OR | OR |
| SelectValue | Enter Value |
| IsEmpty | Is Empty |
| IsNotEmpty | Is Not Empty |
| IsNull | Is Null |
| IsNotNull | Is Not Null |

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", isDefaultActive=true, compileJsx=true %}

```tsx
import { L10n } from '@syncfusion/ej2-base';
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { hardwareData } from '../datasource.ts';

L10n.load({
    'de-DE': {
        'querybuilder': {
            "AddCondition": "Bedingung hinzufügen",
            "AddGroup": "Gruppe hinzufügen",
            "Between": "Zwischen",
            "Contains": "Enthält",
            "DeleteGroup": "Gruppe löschen",
            "DeleteRule": "Entfernen Sie diesen Zustand",
            "Edit": "BEARBEITEN",
            "EndsWith": "Endet mit",
            "Equal": "Gleich",
            "GreaterThan": "Größer als",
            "GreaterThanOrEqual": "Größer als oder gleich",
            "In": "Im",
            "LessThan": "Weniger als",
            "LessThanOrEqual": "Weniger als oder gleich",
            "NotBetween": "Nicht zwischen",
            "NotEqual": "Nicht gleich",
            "NotIn": "Nicht in",
            "Remove": "LÖSCHEN",
            "SelectField": "Wählen Sie ein Feld aus",
            "SelectOperator": "Operator auswählen",
            "StartsWith": "Beginnt mit",
            "ValidationMessage": "Dieses Feld wird benötigt",
        }
    }
});

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
            <QueryBuilderComponent width='100%' locale='de-DE' dataSource={hardwareData} columns={this.columnData} rule={this.importRules} />
        );
    }
}

ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}