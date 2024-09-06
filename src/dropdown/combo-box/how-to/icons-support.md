---
title: "Combo box How to show the list items with icons"
component: "ComboBox"
description: "This section explains how to add icons with combo box options."
---

# Show the list items with icons

You can render **icons** to the list items by mapping the
the [iconCss](../../api/combo-box/#fields) &nbsp;fields.
This `iconCss` field create a span in the list item with mapped class name
to allow styling as per your need.

In the following sample, icon classes are mapped with `iconCss` field.

{% tab template="combobox/icons", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private sortFormatData: { [key: string]: Object }[] = [
        { Class: 'asc-sort', Type: 'Sort A to Z', Id: '1' },
        { Class: 'dsc-sort', Type: 'Sort Z to A ', Id: '2' },
        { Class: 'filter', Type: 'Filter', Id: '3' },
        { Class: 'clear', Type: 'Clear', Id: '4' }
    ];

    // map the icon column to iconCSS field.
    private fields: object = { text: 'Type', iconCss: 'Class', value: 'Id' };

    public render() {
        return (
             // specifies the tag for render the ComboBox component
            <ComboBoxComponent id="comboelement" dataSource={this.sortFormatData} fields={this.fields} placeholder="Select a format" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}
