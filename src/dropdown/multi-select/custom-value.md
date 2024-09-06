---
title: "Multiselect Custom value"
component: "MultiSelect"
description: "This section for Syncfusion react multiselect component demonstrates the addition of a new value that is not present in the predefined list."
---

# CustomValue

The MultiSelect allows user to add a new non-present option to the component value when [`allowCustomValue`](../api/multi-select/#allowcustomvalue) is enabled.
while selecting the new custom value `customValueSelection` event will be triggered.

The following sample demonstrates configuration of custom value support with the MultiSelect component.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { id: 'game1', sports: 'Badminton' },
        { id: 'game2', sports: 'Football' },
        { id: 'game3', sports: 'Tennis' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'sports', value: 'id' };

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" dataSource={this.sportsData} fields={this.fields} placeholder="Select a game"  allowCustomValue={true} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}