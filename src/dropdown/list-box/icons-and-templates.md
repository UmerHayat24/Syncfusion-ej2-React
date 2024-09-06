---
title: "ListBox with icons and customization"
component: "ListBox"
description: "ListBox supports icons, images and customization of each list elements."
---

# Icons and Customization

## Icons

To place the icon on a list box, set the [`iconCss`](../api/list-box/fieldSettingsModel/#iconcss) property to `e-icons` with the required icon CSS. By default, the icon is positioned to the left side of the list.

In the following sample, icon classes are mapped with `iconCss` field.

{% tab template="listbox/icons", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';

export default class App extends React.Component<{}, {}> {
public data: { [key: string]: Object }[] = [
    { text: 'Account Settings', iconCss: 'e-list-icons e-list-user-settings' },
    { text: 'Address Book', iconCss: 'e-list-icons e-list-address-book' },
    { text: 'Delete', iconCss: 'e-list-icons e-list-delete' },
    { text: 'Forward', iconCss: 'e-list-icons e-list-forward' },
    { text: 'Reply', iconCss: 'e-list-icons e-list-reply' },
    { text: 'Reply All', iconCss: 'e-list-icons e-list-reply-all' },
    { text: 'Save All Attachments', iconCss: 'e-list-icons e-list-save-all-attachments' },
    { text: 'Save As', iconCss: 'e-list-icons e-list-icon-save-as' },
    { text: 'Touch/Mouse Mode', iconCss: 'e-list-icons e-list-touch' },
    { text: 'Undo', iconCss: ' e-list-icons e-list-undo' }
];

private fields:object = { text:"text", iconCss:"iconCss"}
render() {
  return (
    <ListBoxComponent dataSource={this.data} fields={this.fields}/>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Templates

ListBox items can be customized according to the requirement using [`itemTemplate`](../api/list-box/#itemtemplate) property.

In the following sample, the items in the cart are displayed using list box template,

{% tab template="listbox/template", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';

export default class App extends React.Component<{}, {}> {
public data: { [key: string]: Object }[] = [
    { text: 'JavaScript', pic: 'javascript', description: 'It is a lightweight interpreted or JIT-compiled programming language.' },
    { text: 'TypeScript', pic: 'typeScript', description: 'It is a typed superset of Javascript that compiles to plain JavaScript.' },
    { text: 'Angular', pic: 'angular', description: 'It is a TypeScript-based open-source web application framework.' },
    { text: 'React', pic: 'react', description: 'A JavaScript library for building user interfaces. It can also render on the server using Node.' },
    { text: 'Vue', pic: 'vue', description: 'A progressive framework for building user interfaces. it is incrementally adoptable.' }
];

render() {
  return (
  <div>
    <ListBoxComponent dataSource={this.data} itemTemplate='<div class="list-wrapper"><span class="${pic} e-avatar e-avatar-xlarge e-avatar-circle"></span><span class="text">${text}</span><span class="description">${description}</span></div>'/>
  </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}