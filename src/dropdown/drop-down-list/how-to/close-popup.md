---
title: "Drop-down list How to close popup on scroll"
component: "DropDownList"
description: "This section explains on how to close popup on scroll in the Syncfusion React drop-down list component."
---

# Close the popup on scroll

By using the `hidePopup` method in DropDownList, you can close the popup on scroll when triggered the windows scroll event.

The following example demonstrate about how to close the popup on scroll.

{% tab template="dropdownlist/how-to", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  private dropDownListObject: any;
  // define the data with category
  private sportsData: { [key: string]: Object }[] = [
    'Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
  constructor(props: any){
      super(props);
     window.addEventListener('scroll', this.handleScroll.bind(this));
  }  
  // on scroll event
  public handleScroll() {
    this.dropDownListObject.hidePopup();
  }
  public render() {
    return (

      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" ref={(scope) => { this.dropDownListObject = scope; }} dataSource={this.sportsData} placeholder="Select a game" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}