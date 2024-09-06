---
title: "ListView Checklist"
component: "ListView"
description: "React listview supports check-list (list-view with checkbox) feature to select single or multiple list items."
---

# Checklist

The ListView supports checkbox in default and group-lists which is used to select multiple items.
The checkbox can be enabled by the `showCheckBox` property.

The Checkbox will be useful in the scenario where we need to select multiple options. For Example,
In Shipping cart we can be able to select or unselect the desired items before checkout and also
it will be useful in selecting multiple items that belongs to same category using the group list.

{% tab template="listview/checklist", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
    //define the array of JSON
    private data: { [key: string]: Object }[] = [
        {text: 'Do Meditation', id: '1'},
        {text: 'Go Jogging', id: '2'},
        {text: 'Buy Groceries', id: '3'},
        {text: 'Pay Phone bill', id: '4'},
        {text: 'Play Football with your friends', id: '5'},
    ];

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id='list' dataSource={this.data} showCheckBox = {true} headerTitle='TO DO LIst' showHeader={true}></ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Checkbox Position

In ListView the checkbox can be positioned into either `Left` or `Right` side of the list-item text.
This can be achieved by `checkBoxPositon` property. By default, checkbox will be positioned to `Left` of list-item text.

{% tab template="listview/checklist", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  //define the array of JSON
  private settings: { [key: string]: Object }[] = [
    { text: "Hennessey Venom", id: "list-01" },
    { text: "Bugatti Chiron", id: "list-02" },
    { text: "Bugatti Veyron Super Sport", id: "list-03" },
    { text: "SSC Ultimate Aero", id: "list-04" },
    { text: "Koenigsegg CCR", id: "list-05" },
    { text: "McLaren F1", id: "list-06" },
    { text: "Aston Martin One- 77", id: "list-07" },
    { text: "Jaguar XJ220", id: "list-08" },
    { text: "McLaren P1", id: "list-09" },
    { text: "Ferrari LaFerrari", id: "list-10" }
  ];
  private fields = { text: "text", id: "id" };
  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent
        id="list"
        dataSource={this.settings}
        fields={this.fields}
        showCheckBox={true}
        checkBoxPosition="Right"
      />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
