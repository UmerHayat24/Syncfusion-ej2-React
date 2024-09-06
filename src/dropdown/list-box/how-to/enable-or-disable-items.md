---
title: "Enable or disable items in list box"
component: "ListBox"
description: "ListBox component supports customization of menu items so that the items can be enabled or disabled."
---

# Enable or disable items

To enable or disable items in the list box, [`enableItems`](../api/list-box/#enableitems) method can be used. In the following example, the `Bugatti Veyron Super Sport` and `SSC Ultimate Aero` items are disabled by default and by clicking `Enable Items` buttons, the disabled items will be enabled.

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
public listboxobj:ListBoxComponent;
    public enableitem(): void {
    this.listboxobj.enableItems(['Bugatti Veyron Super Sport', 'SSC Ultimate Aero'], true);
    }
    public created():void {
      this.listboxobj.enableItems(['Bugatti Veyron Super Sport', 'SSC Ultimate Aero'], false);
    }
  render() {
    return (
    <div>
      <ListBoxComponent dataSource={this.data} ref={(scope) => this.listboxobj = scope as ListBoxComponent} created={this.created.bind(this)} />
      <ButtonComponent onClick={this.enableitem.bind(this)}>Enable Items</ButtonComponent>
    </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}