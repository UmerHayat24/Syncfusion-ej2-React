---
title: "Group items in Popup"
component: "SplitButton"
description: "React SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Group items in Popup

Items in popup can be grouped in SplitButton by templating entire popup with ListView. To achieve grouping in ListView, check [`ListView grouping`](../../listview/grouping#grouping) documentation. To template ListView in popup, create ListView with id `listview` and provide it as
[`target`](../../api/split-button#target) for SplitButton.

The following example illustrates how to group items in popup using ListView component.

{% tab template= "split-button/listview", sourceFiles="app/**/*.tsx,index.html,style.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SplitButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render SplitButton.
class App extends React.Component<{}, {}> {

    // Datasource for listview.
    public listItems: Array<{ [key: string]: string; }> = [
        {
            'category': 'Basic',
            'text': 'Cut'
        },
        {
            'category': 'Basic',
            'text': 'Copy',
        },
        {
            'category': 'Basic',
            'text': 'Paste'
        },
        {
            'category': 'Advanced',
            'text': 'Paste as Formula'
        },
        {
            'category': 'Advanced',
            'text': 'Paste as Hyperlink'
        },
    ];

    public field: any = { groupBy: 'category' };

  public render() {
    return (
    <div>
       <ListViewComponent id="listview" dataSource={this.listItems} fields={this.field} sortOrder="Descending"/>
       <SplitButtonComponent target="#listview">ClipBoard</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}