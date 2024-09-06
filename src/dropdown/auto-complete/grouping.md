---
title: "Autocomplete Grouping"
component: "AutoComplete"
description: "This section for Syncfusion react autocomplete component demonstrates the grouping with individual header and it's header customization."
---

# Grouping

The AutoComplete supports wrapping nested elements into a group based on different categories. The category of each list
item can be mapped through the [groupBy](../api/auto-complete/#fields) field in the data table.
The group header is displayed both as inline and fixed headers. The fixed group header content is updated dynamically on scrolling
the popup list with its category value.

In below sample, vegetables are grouped based on its category using `groupBy` field.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
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
        { Vegetable: 'Horse gram', Category: 'Beans', Id: 'item8' }
    ];

    // map the groupBy field with Category column
    private fields: object = { groupBy: 'Category', value: 'Vegetable' };

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" fields={this.fields} dataSource={this.vegetableData} placeholder="Select a vegetable" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Customization

The grouping header is also provided with customization option. This allows custom designing using the
groupTemplate property for both inline and fixed headers as referred here

[groupTemplate](../api/auto-complete/#grouptemplate) property for both inline and
fixed header.

## See Also

* [Group Template support to AutoComplete](./templates#group-template).