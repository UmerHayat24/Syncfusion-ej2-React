---
title: "Combo box autofill"
component: "ComboBox"
description: "This section explains how to acheive autofill functionality in combo box control."
---

# Autofill supports with ComboBox

The ComboBox supports the `autofill` behaviour with the help of
[autofill](../../api/combo-box/#autofill) property. Whenever you change
the input value, the ComboBox will autocomplete your data by matching the typed character. Suppose, if no
matches found then, ComboBox doesn't suggest any item.

The following examples, showcase that how to work autofill with ComboBox.

{% tab template="combobox/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // define the array of data
  private sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];

  public render() {
    return (
        // specifies the tag for render the ComboBox component
      <ComboBoxComponent id="comboelement" placeholder="Select a game" autofill={true} dataSource={this.sportsData} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));
```

{% endtab %}
