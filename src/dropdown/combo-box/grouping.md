---
title: "Combo box Grouping"
component: "ComboBox"
description: "This section Syncfusion react combo box component shows the grouping with individual header and it's header customization."
---

# Grouping

The ComboBox supports wrapping nested elements into a group based on different categories. The category
of each list item can be mapped through the
[groupBy](../api/combo-box/#fields) &nbsp;field in
the data table. The group header is displayed both as inline and fixed headers. The fixed group header content
is updated dynamically on scrolling the popup list with its category value.

In the following sample, the vegetables are grouped according on its category using `groupBy` field.

{% tab template="combobox/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the data with category
    private vegetableData: { [key: string]: Object }[] = [
        { Vegetable: 'Cabbage', Category: 'Leafy and Salad', Id: 'item1' },
        { Vegetable: 'Spinach', Category: 'Leafy and Salad', Id: 'item2' },
        { Vegetable: 'Wheat grass', Category: 'Leafy and Salad', Id: 'item3' },
        { Vegetable: 'Yarrow', Category: 'Leafy and Salad', Id: 'item4' },
        { Vegetable: 'Pumpkins', Category: 'Leafy and Salad', Id: 'item5' },
        { Vegetable: 'Chickpea', Category: 'Beans', Id: 'item6' },
        { Vegetable: 'Green bean', Category: 'Beans', Id: 'item7' },
        { Vegetable: 'Horse gram', Category: 'Beans', Id: 'item8' },
        { Vegetable: 'Garlic', Category: 'Bulb and Stem', Id: 'item9' },
        { Vegetable: 'Nopal', Category: 'Bulb and Stem', Id: 'item10' },
        { Vegetable: 'Onion', Category: 'Bulb and Stem', Id: 'item11' }
    ];

    // map the groupBy field with Category column
    private fields: object = { groupBy: 'Category', text: 'Vegetable', value: 'Id' };

    public render() {
        return (
             // specifies the tag for render the ComboBox component
            <ComboBoxComponent id="comboelement" popupHeight='200px' fields={this.fields} dataSource={this.vegetableData} placeholder="Select a vegetable" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Customization

The grouping header is also provided with customization option. This allows custom designing using
the `groupTemplate` property for both inline and fixed headers as referred here:
[Group Template support to ComboBox](/combo-box/templates/#group-template).

## See Also

* [Group Template support to ComboBox](./templates#group-template).