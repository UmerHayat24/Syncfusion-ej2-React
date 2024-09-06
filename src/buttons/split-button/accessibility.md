---
title: "SplitButton Accessibility"
component: "SplitButton"
description: "React SplitButton component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

## ARIA attributes

The web accessibility makes web content and web applications more accessible for people with disabilities.
It especially helps in dynamic content change and development of advanced user interface controls with AJAX, HTML, JavaScript, and related technologies.
SplitButton provides built-in compliance with `WAI-ARIA` specifications. `WAI-ARIA` support is achieved through the
attributes like `aria-expanded`, `aria-owns` and `aria-haspopup` applied for action item in SplitButton.
It helps the people with disabilities by providing information about the widget for assistive
technology in the screen readers. SplitButton component contains the  `menuItem` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| menuItem | This role will be specified for an action items. |
| aria-haspopup | Indicates the availability and type of interactive splitbutton popup element. |
| aria-expanded | Indicates whether the splitbutton popup can be expanded or collapsed, as well as indicates whether its current state is expanded or collapsed. |
| aria-owns | Identifies an elements in order to define a visual, functional, or contextual parent/child relationship between DOM elements where the DOM hierarchy cannot be used to represent the relationship. |

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
Closes the opened popup.</td></tr>
<tr>
<td>
<kbd>Enter</kbd></td><td>
Opens the popup, or activates the highlighted item and closes the popup.</td></tr>
<tr>
<td>
<kbd>Space</kbd></td><td>
Opens the popup.</td></tr>
<tr>
<td>
<kbd>Up</kbd></td><td>
Navigates up or to the previous action item.</td></tr>
<tr>
<td>
<kbd>Down</kbd></td><td>
Navigates down or to the next action item.</td></tr>
<tr>
<td>
<kbd>Alt + Up Arrow</kbd></td><td>
Opens the popup.</td></tr>
<tr>
<td>
<kbd>Alt + Down Arrow</kbd></td><td>
Closes the popup.</td></tr>
</table>

{% tab template= "split-button/accessibility", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

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
        iconCss: 'e-sb-icons e-cut',
        text: 'Cut'
    },
    {
        iconCss: 'e-icons e-copy',
        text: 'Copy'
    },
    {
        iconCss: 'e-sb-icons e-paste',
        text: 'Paste'
    }];
  public render() {
    return (
    <div>
       <SplitButtonComponent iconCss= "e-sb-icons e-paste" items = {this.items}>Paste</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}