---
title: "SplitButton Popup Items"
component: "SplitButton"
description: "React SplitButton allows the end user to customize the whole popup or action items in popup using templates, and to place icons in popup items."
---

# Popup Items

## Icons

The Popup action item have an icon or image to provide visual representation of the action. To place the icon on a popup item,
set the [`iconCss`](../api/split-button#iconcss) property to `e-icons` with the required icon CSS. By default,
the icon is positioned to the left side of the popup action item.

In the following sample, the icons for Cut, Copy, and Paste menu items are
added using the iconCss property

{% tab template= "split-button/popup-icon", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

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
       <SplitButtonComponent items = {this.items} iconCss= 'e-sb-icons e-paste'>Paste</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}

## Template

### Item Templating

Popup items can be customized by using the [`beforeItemRender`](../api/split-button#beforeitemrender) event. The item render
event triggers while rendering each Popup action item. The event argument will be used to identify the action item and customize it based
on the requirement.

{% tab template= "split-button/template", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { createElement, enableRipple } from '@syncfusion/ej2-base';
import { ItemModel, MenuEventArgs, SplitButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render SplitButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Cut',
    },
    {
        text: 'Copy',
    },
    {
        text: 'Paste',
    }];
  public itemBeforeEvent: any = (args: MenuEventArgs) => {
      const shortCutSpan = createElement('span');
      const text = args.item.text;
      args.element.appendChild(shortCutSpan);
      shortCutSpan.setAttribute('class','shortcut');
      const clsName = (text === 'Copy') ? 'e-icons' : 'e-sb-icons';
      shortCutSpan.classList.add(clsName);
      (text === 'Cut') ? shortCutSpan.classList.add('e-cut') : (text === 'Paste') ? shortCutSpan.classList.add('e-paste') : shortCutSpan.classList.add('e-copy');
  }
  public render() {
    return (
    <div>
       <SplitButtonComponent items = {this.items} beforeItemRender= {this.itemBeforeEvent} iconCss= 'e-sb-icons e-paste'/>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}

### Popup Templating

The whole popup can be customized as per the requirement. In the following example, the popup can be
customized by handling it in [`target`](../api/split-button#target) property.

{% tab template= "split-button/popup-template", sourceFiles="app/**/*.tsx,index.html,style.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SplitButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render SplitButton.
class App extends React.Component<{}, {}> {
  public render() {
    return (
    <div>
        <div id='dropdowntarget'>
          <div id= "first">
              <div id='black'/>
              <div id='red'/>
              <div id='green'/>
              <div id='gray'/>
              <div id='blue'/>
              <div id='violet'/>
              <div id='brown'/>
              <div id='darkgoldenrod'/>
              <div id='aquamarine'/>
          </div>
        </div>
        <SplitButtonComponent target='#dropdowntarget' iconCss= 'e-sb-icons e-color'/>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}

## See Also

* [Popup items grouping](./how-to/group-items-in-popup)
* [SplitButton popup with separator](./icons-and-separator#separator)