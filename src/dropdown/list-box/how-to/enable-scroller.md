---
title: "ListBox Scroller"
component: "ListBox"
description: "ListBox component has support to scroll the list items."
---

# Enable Scroller

The ListBox supports scrolling and it can be achieved by restricting the height of the list box using [`height`](../api/list-box/#height) property.

In the following sample, `height` of the list box is restricted to `290px`.

{% tab template="listbox/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';

export default class App extends React.Component<{}, {}> {
   private data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
];
  render() {
    return (
      <ListBoxComponent dataSource={this.data} height="290px"/>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}