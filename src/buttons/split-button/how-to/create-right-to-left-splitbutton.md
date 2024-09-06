---
title: "Create right-to-left SplitButton"
component: "SplitButton"
description: "React SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Create right-to-left SplitButton

SplitButton component has RTL support. This can be achieved by setting [`enableRtl`](../../api/split-button#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in SplitButton component.

{% tab template= "split-button/howto", sourceFiles="app/**/*.tsx,index.html,style.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ItemModel, SplitButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render SplitButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Autosum'
    },
    {
        text: 'Average'
    },
    {
        text: 'Count numbers'
    },
    {
        text: 'Min'
    },
    {
        text: 'Max'
    }];
  public render() {
    return (
    <div>
       <SplitButtonComponent items = {this.items} enableRtl ={true} iconCss= 'e-sb e-sigma'>Autosum</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}