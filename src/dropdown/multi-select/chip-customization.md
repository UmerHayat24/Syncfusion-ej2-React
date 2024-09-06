---
title: "Multiselect Chip Customization"
component: "MultiSelect"
description: "This section for Syncfusion react multiselect component demonstrates on how to customize the selected chip element when select."
---

# Chip Customization

The MultiSelect allows the user to customize the selected chip element through the [`tagging`](../api/multi-select/#tagging)
event. In that event, you can set the custom classes to chip element via that event argument of `setClass` method.

The following sample demonstrates chip-customization with the MultiSelect component.

{% tab template="multiselect/chip-customization", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { MultiSelectComponent, TaggingEventArgs } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // define the JSON of data
  private colorsData: { [key: string]: Object }[] =[
    { Color: 'Chocolate', Code: '#75523C' },
    { Color: 'CadetBlue', Code: '#3B8289' },
    { Color: 'DarkOrange', Code: '#FF843D' },
    { Color: 'DarkRed', Code: '#CA3832' },
    { Color: 'Fuchsia', Code: '#D44FA3' },
    { Color: 'HotPink', Code: '#F23F82' },
    { Color: 'Indigo', Code: '#2F5D81' },
    { Color: 'LimeGreen', Code: '#4CD242' },
    { Color: 'OrangeRed', Code: '#FE2A00' },
    { Color: 'Tomato', Code: '#FF745C' }
];
  // maps the appropriate column to fields property
  private fields: { [key: string]: string } = { text: 'Color', value: 'Code' };
  // set the value to MultiSelect
  private colorValues: string[] = ['#75523C', '#4CD242', '#FF745C'];
  // bind the tagging event
  public onTagging = (e: TaggingEventArgs) => {
    // set the current selected item text as class to chip element.
    e.setClass((e.itemData as any)[this.fields.text].toLowerCase());
  }
  public render() {
    return (
            <MultiSelectComponent id="chip-customization" value={this.colorValues} dataSource={this.colorsData} fields={this.fields} mode="Box" placeholder="Favorite Colors" tagging={this.onTagging = this.onTagging.bind(this)} />

    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}