---
title: "Form submit to the list box"
component: "ListBox"
description: "ListBox component supports form submit to the list box."
---

# Form submit to the list box

In the following code snippet, the value that is in selected state will be sent on form submit.

{% tab template="listbox/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

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
    <form>
      <ListBoxComponent dataSource={this.data}/>
      <ButtonComponent isPrimary="true" content="Submit"></ButtonComponent>
    </form>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}