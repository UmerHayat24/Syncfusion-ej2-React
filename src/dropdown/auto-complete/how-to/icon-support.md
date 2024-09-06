---
title: "Autocomplete How to show the list items with icons"
component: "AutoComplete"
description: "This section explains how to add icons with autocomplete options."
---

# Show the list items with icons

You can render **icons** to the list items by mapping the [`iconCss`](../../api/auto-complete/#fields) field.
This `iconCss` field create a span in the list item with mapped class name to allow styling as per your need.

In the following sample, icon classes are mapped with iconCss field.

{% tab template="autocomplete/icons", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private fields: object = { value: 'Type', iconCss: 'Class' };

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="" dataSource={this.sortFormatData} fields={this.fields} placeholder="Find a format" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}