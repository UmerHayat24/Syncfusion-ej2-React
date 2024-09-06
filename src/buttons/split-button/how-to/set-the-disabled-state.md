---
title: "Set the disabled state"
component: "SplitButton"
description: "React SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Set the disabled state

SplitButton component can be enabled or disabled using [`disabled`](../../api/split-button#disabled) property.
To disable SplitButton component, set the disabled property as true.

The following example illustrates how to set the disable state in SplitButton component.

{% tab template= "split-button/disabled", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SplitButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
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
        text: 'Count numbers',
    },
    {
        text: 'Min'
    },
    {
        text: 'Max'
    }];
  render() {
    return (
    <div>
       <SplitButtonComponent items = {this.items} disabled ={true} iconCss= 'e-sb e-sigma'>Autosum</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}