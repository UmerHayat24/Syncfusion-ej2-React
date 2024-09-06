---
title: "Drop-down list How to clear the list item"
component: "DropDownList"
description: "This section explains on how to clear the selected items of the Syncfusion react drop-down list component."
---

# Clear the selected item in DropDownList

You can clear the selected item in the below two different ways.

By clicking on the `clear icon` which is shown in DropDownList element, you can clear the selected item in
DropDownList through **interaction**. By using [`showClearButton`](../../api/drop-down-list/#showclearbutton)
property, you can enable the clear icon in DropDownList element.

Through **programmatic** you can set `null` value to anyone of the index, text or value property to clear the selected item in DropDownList.

The following example demonstrate about how to clear the selected item in DropDownList.

{% tab template="dropdownlist/clear-text", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  private dropDownListObject: any;
  private sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
  public onclick() {
    this.dropDownListObject.value = null;
  }
  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <div>
        <DropDownListComponent id="ddlelement" ref={(scope) => { this.dropDownListObject = scope; }} dataSource={this.sportsData} placeholder="Select a game" />
        <button id='btn' className="e-control e-btn" onClick={this.onclick = this.onclick.bind(this)}> Set null to value property</button>
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}