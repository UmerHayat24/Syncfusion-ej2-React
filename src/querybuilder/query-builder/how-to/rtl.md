---
title: "Right to Left suppport in Query Builder"
component: "Query Builder"
description: "This section helps to learn how to display React QueryBuilder Component in RTL mode."
---

# Right to left (RTL)

RTL provides an option to switch the text direction and layout of the Query Builder component from right to left. It improves the user experiences and accessibility for users who use right-to-left languages (Arabic, Farsi, Urdu, etc.). To enable RTL, set the [`enableRtl`](https://ej2.syncfusion.com/react/documentation/right-to-left/) to true.

{% tab template="query-builder/default", sourceFiles="app/**/*.tsx,index.html,datasource.ts", isDefaultActive=true, compileJsx=true %}

```tsx
import { L10n } from '@syncfusion/ej2-base';
import { ColumnsModel, QueryBuilderComponent, RuleModel } from '@syncfusion/ej2-react-querybuilder';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { hardwareData } from '../datasource.ts';

L10n.load({
    'ar-AE': {
        'querybuilder': {
            'AddCondition': 'اضافة الشرط',
            'AddGroup': 'إضافة مجموعة',
            'Between': 'ما بين',
            'Contains': 'يحتوي على',
            'DeleteGroup': 'حذف المجموعة',
            'DeleteRule': 'أزل هذا الشرط',
            'Edit': 'تصحيح',
            'EndsWith': 'ينتهي مع',
            'Equal': 'مساو',
            'GreaterThan': 'أكثر من',
            'GreaterThanOrEqual': 'أكبر من أو يساوي',
            'In': 'في',
            'LessThan': 'أقل من',
            'LessThanOrEqual': 'اصغر من او يساوي',
            'NotBetween': 'ليس بينهما',
            'NotEqual': 'ليس متساوي',
            'NotIn': 'ليس في',
            'Remove': 'إزالة',
            'SelectField': 'اختر مجال',
            'SelectOperator': 'حدد المشغل',
            'StartsWith': 'ابدا ب',
            'ValidationMessage': 'هذه الخانة مطلوبه'
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
            <QueryBuilderComponent width='100%' locale='ar-AE' enableRtl={true} dataSource={hardwareData} columns={this.columnData} rule={this.importRules} />
        );
    }
}

ReactDom.render(<App />,document.getElementById('querybuilder'));
```

{% endtab %}