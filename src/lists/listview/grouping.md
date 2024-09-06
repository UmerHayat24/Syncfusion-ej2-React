---
title: "ListView Grouping"
component: "ListView"
description: "React listView component supports grouping feature that helps group the logically related items under a category."
---

# Grouping

ListView supports to wrap the nested element into a group based on category.

The category of each list item can be mapped with groupBy field in the data table, which also supports single-level navigation.

In below sample, Cars are grouped based on its category using groupBy field.

{% tab template="listview/grouping", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  // define the array of Json
  private arts: { [key: string]: string }[] = [
    {
        'text': 'Audi A4',
        'id': '9bdb',
        'category': 'Audi'
    },
    {
        'text': 'Audi A5',
        'id': '4589',
        'category': 'Audi'
    },
    {
        'text': 'BMW 501',
        'id': 'f849',
        'category': 'BMW'
    },
    {
        'text': 'BMW 502',
        'id': '7aff',
        'category': 'BMW'
    }
  ];

  private fields = { groupBy: 'category', tooltip: 'text' };
  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id='list' dataSource={this.arts} fields={this.fields} ></ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Customization

The grouping header can be customized by using groupTemplate property for both inline and fixed group header.