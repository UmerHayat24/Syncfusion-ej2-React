---
title: "Adding items to the list box"
component: "ListBox"
description: "ListBox component supports adding of items to the list box."
---

# Add items to the list box

To add an item or multiple items, [`addItems`](../api/list-box/#additems) method can be used. In the following example, the `Bugatti Veyron Super Sport` and `SSC Ultimate Aero` items will be added while clicking `Add Items` button.

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
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
];
public listboxobj:ListBoxComponent;
    public btnClick(): void {
    if(!this.listboxobj.getDataByValue("Bugatti Veyron Super Sport")){
        this.listboxobj.addItems([{ text: 'Bugatti Veyron Super Sport', id: 'list-03' }, { text: 'SSC Ultimate Aero', id: 'list-04' }]);
    }
    }
  render() {
    return (
      <div>
      <ListBoxComponent dataSource={this.data} ref={(scope) => this.listboxobj = scope as ListBoxComponent} />
      <ButtonComponent onClick={this.btnClick.bind(this)}>Add Items</ButtonComponent>
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}