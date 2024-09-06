---
title: "ContextMenu Accessibility"
component: "ContextMenu"
description: "The ContextMenu control has accessibility support to access the features via keyboard, screen readers, or other assistive technology devices."
---

# Accessibility

## ARIA attributes

The web accessibility makes web content and web applications more accessible for people
with disabilities. It especially helps in dynamic content change and development of advanced user interface
controls with AJAX, HTML, JavaScript, and related technologies.
ContextMenu provides built-in compliance with `WAI-ARIA` specifications. `WAI-ARIA` support is
achieved through the attributes like `aria-expanded`, `aria-haspopup` applied for menu item in
ContextMenu. It helps the people with disabilities by providing information about the widget for assistive
technology in the screen readers. ContextMenu component contains the `menu` role and `menuItem` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| menu | This role will be specified for an item which have sub menu. |
| menuItem | This role will be specified for an item which do not have sub menus. |
| aria-haspopup | Indicates the availability and type of interactive popup element. |
| aria-expanded | Indicates whether the subtree can be expanded or collapsed, as well as whether its current state is expanded or collapsed. |

## Keyboard interaction

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
<b>Keyboard shortcuts</b></td><td>
<b>Actions</b></td></tr>
<tr>
<td>
<kbd>Esc</kbd></td><td>
Closes the opened ContextMenu.</td></tr>
<tr>
<td>
<kbd>Enter</kbd></td><td>
Selects the focused item.</td></tr>
<tr>
<td>
<kbd>Up</kbd></td><td>
Navigates up or to the previous menu item.</td></tr>
<tr>
<td>
<kbd>Down</kbd></td><td>
Navigates down or to the next menu item.</td></tr>
<tr>
<td>
<kbd>Left</kbd></td><td>
Close the current sub menu and navigates to parent menu..</td></tr>
<tr>
<td>
<kbd>Right</kbd></td><td>
Navigates and open the next sub menu.</td></tr>
</table>

{% tab template="context-menu/accessibility", isDefaultActive = "true",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public cmenu: ContextMenuComponent;
    public menuItems: MenuItemModel[] = [
      {
        iconCss: 'e-menu-icons e-cut',
        text: 'Cut'
      },
      {
        iconCss: 'e-icons e-copy',
        text: 'Copy'
      },
      {
          iconCss: 'e-menu-icons e-paste',
          items: [
              {
                iconCss: 'e-cm-icons e-pastetext',
                text: 'Paste Text',
              },
              {
                iconCss: 'e-cm-icons e-pastespecial',
                text: 'Paste Special'
              }
          ],
          text: 'Paste'
      }];
    constructor(props: any) {
        super(props);
        this.onCreated = this.onCreated.bind(this);
    }
    public onCreated(){
      this.cmenu.open(40, 20);
    }
  
  public render() {
      return (
        <div className="container">
         <div id='target'>Right click / Touch hold to open the ContextMenu</div>
          <ContextMenuComponent ref= {(scope) => this.cmenu = scope as ContextMenuComponent} id='contextmenu' items={this.menuItems} created={this.onCreated}/>
        </div>
      );
    }
  }
ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
