---
title: "Multiselect Checkbox"
component: "MultiSelect"
description: "This sample for Syncfusion react multiselect component demonstrates the built-in support to select the multiple values through checkbox."
---

# CheckBox

The MultiSelect has built-in support to select multiple values through checkbox,
when [`mode`](../api/multi-select/#mode) property set as `CheckBox`.

To use checkbox, inject the `CheckBoxSelection` module in the MultiSelect.

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { CheckBoxSelection, Inject, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { Id: 'game1', Game: 'Badminton' },
        { Id: 'game2', Game: 'Football' },
        { Id: 'game3', Game: 'Tennis' },
        { Id: 'game4', Game: 'Golf' },
        { Id: 'game5', Game: 'Cricket' },
        { Id: 'game6', Game: 'Handball' },
        { Id: 'game7', Game: 'Karate' },
        { Id: 'game8', Game: 'Fencing' },
        { Id: 'game9', Game: 'Boxing' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'Game', value: 'Id' };

    public render() {
        return (
            // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="checkbox" dataSource={this.sportsData}
                fields={this.fields} placeholder="Select game" mode="CheckBox">
                <Inject services={[CheckBoxSelection]} />
            </MultiSelectComponent>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Select All

The MultiSelect component has in-built support to select the all list items using `Select All` options in the header.

When the [`showSelectAll`](../api/multi-select/#showselectall)
property is set to true, by default Select All text will show.
You can customize the name attribute of the Select All option by using
[`selectAllText`](../api/multi-select/#selectalltext).

For the unSelect All option, by default unSelect All text will show.
You can customize the name attribute of the unSelect All option by using
[`unSelectAllText`](../api/multi-select/#unselectalltext).

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { CheckBoxSelection, Inject, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { Id: 'game1', Game: 'Badminton' },
        { Id: 'game2', Game: 'Football' },
        { Id: 'game3', Game: 'Tennis' },
        { Id: 'game4', Game: 'Golf' },
        { Id: 'game5', Game: 'Cricket' },
        { Id: 'game6', Game: 'Handball' },
        { Id: 'game7', Game: 'Karate' },
        { Id: 'game8', Game: 'Fencing' },
        { Id: 'game9', Game: 'Boxing' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'Game', value: 'Id' };

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="checkbox" dataSource={this.sportsData}
                fields={this.fields} placeholder="Select game" mode="CheckBox" selectAllText="Select All" unSelectAllText="unSelect All" showSelectAll={true}>
                <Inject services={[CheckBoxSelection]} />
            </MultiSelectComponent>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Selection Limit

Defines the limit of the selected items using [`maximumSelectionLength`](../api/multi-select/#maximumselectionlength).

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { CheckBoxSelection, Inject, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { Id: 'game1', Game: 'Badminton' },
        { Id: 'game2', Game: 'Football' },
        { Id: 'game3', Game: 'Tennis' },
        { Id: 'game4', Game: 'Golf' },
        { Id: 'game5', Game: 'Cricket' },
        { Id: 'game6', Game: 'Handball' },
        { Id: 'game7', Game: 'Karate' },
        { Id: 'game8', Game: 'Fencing' },
        { Id: 'game9', Game: 'Boxing' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'Game', value: 'Id' };

    public render() {
        return (
            // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="checkbox" dataSource={this.sportsData}
                fields={this.fields} placeholder="Select game" mode="CheckBox" maximumSelectionLength={3}>
                <Inject services={[CheckBoxSelection]} />
            </MultiSelectComponent>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Selection Reordering

Using [`enableSelectionOrder`](../api/multi-select/#enableselectionorder) to Reorder the selected items in popup visibility state.

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { CheckBoxSelection, Inject, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { Id: 'game1', Game: 'Badminton' },
        { Id: 'game2', Game: 'Football' },
        { Id: 'game3', Game: 'Tennis' },
        { Id: 'game4', Game: 'Golf' },
        { Id: 'game5', Game: 'Cricket' },
        { Id: 'game6', Game: 'Handball' },
        { Id: 'game7', Game: 'Karate' },
        { Id: 'game8', Game: 'Fencing' },
        { Id: 'game9', Game: 'Boxing' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'Game', value: 'Id' };

    public render() {
        return (
                // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="checkbox" dataSource={this.sportsData}
                fields={this.fields} placeholder="Select game" mode="CheckBox" enableSelectionOrder={false}>
                <Inject services={[CheckBoxSelection]} />
            </MultiSelectComponent>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)
* [How to filter the bound data](./filtering/)
* [How to add custom value to the MultiSelect](./custom-value/)
* [How to render grouping with checkbox](./grouping/#grouping-with-checkbox).