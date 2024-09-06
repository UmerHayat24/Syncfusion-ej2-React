---
title: "Autocomplete custom highlight search"
component: "AutoComplete"
description: "This section explains custom highlight search of autocomplete control."
---

# Custom highlight search

The AutoComplete has built-in support to highlight the searched characters on suggested list items when
enabled the [`highlight`](../../api/auto-complete/#highlight) property.

In the below sample, to customize the matched character in suggestion list by `e-highlight` class.

{% tab template="autocomplete/highlight", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
       { Id: 'Game1', Game: 'Badminton' },
       { Id: 'Game2', Game: 'Basketball' },
       { Id: 'Game3', Game: 'Cricket' },
       { Id: 'Game4', Game: 'Football' },
       { Id: 'Game5', Game: 'Golf' },
       { Id: 'Game6', Game: 'Hockey' },
       { Id: 'Game7', Game: 'Rugby' },
       { Id: 'Game8', Game: 'Snooker' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { value: 'Game' };

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" dataSource={this.sportsData} fields={this.fields} placeholder="Find a game" highlight={true} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}