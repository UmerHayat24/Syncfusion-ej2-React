---
title: "Change Animation Settings in ContextMenu"
component: "ContextMenu"
description: "This section helps to learn how to change animation settings in ContextMenu."
---

# Change animation settings

To change the animation of the ContextMenu, [`animationSettings`](https://ej2.syncfusion.com/react/documentation/api/context-menu/menuAnimationSettingsModel/) property is used.
The supported effects for ContextMenu are,

| Effect | Functionality |
| ------------ | ----------------------- |
| None | Specifies the sub menu transform with no animation effect. |
| SlideDown | Specifies the sub menu transform with slide down effect. |
| ZoomIn | Specifies the sub menu transform with zoom in effect. |
| FadeIn | Specifies the sub menu transform with fade in effect. |

The following sample illustrates how to open ContextMenu with `FadeIn` effect with the `duration` of `800ms`.

{% tab template="context-menu/getting-started",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component {
  private animation: any = {
    duration: 800,
    effect: 'FadeIn'
  };
  private menuItems: MenuItemModel[] = [
    {
        text: 'Show All Bookmarks'
    },
    {
        items: [
            {
                items: [
                    {
                        text: 'Google'
                    },
                    {
                        text: 'Gmail'
                    }
                ],
                text: 'Most Visited'
            },
            {
                text: 'Recently Added'
            }
        ],
        text: 'Bookmarks Toolbar'
    }];

  public render() {
    return (
            <div className="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target'
              items={this.menuItems} animationSettings={this.animation}/>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
