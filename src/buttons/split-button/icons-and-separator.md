---
title: "SplitButton Icons and Separator"
component: "SplitButton"
description: "React SplitButton allows the end user to place the icons and separate popup items in SplitButton."
---

# Icons and separator

## SplitButton icons

SplitButton can have an icon to provide the visual representation of the action. To place the icon on a SplitButton,
set the [`iconCss`](../api/split-button#iconcss) property to `e-icons` with the required icon CSS.
By default, the icon is positioned to the left side of the SplitButton. You can customize the icon's position by
using the [`iconPosition`](../api/split-button#iconposition) property

The following example illustrates how to place icon in SplitButton component.

{% tab template= "split-button/icon", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

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
        text: 'Cut',
    },
    {
        text: 'Copy',
    },
    {
        text: 'Paste',
    }];
  public render() {
    return (
    <div>
       <SplitButtonComponent items = {this.items} iconCss= 'e-sb-icons e-paste'>Paste</SplitButtonComponent>
       <SplitButtonComponent items = {this.items} iconPosition= "Top" iconCss= 'e-sb-icons e-paste'>Paste</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the SplitButton using the [`iconCss`](../api/split-button#iconcss) property.

### Vertical button

Vertical Button in SplitButton can be achieved by adding `e-vertical` class
using [`cssClass`](../api/split-button#cssclass) property.

The following example illustrates how to vertical support in SplitButton component.

{% tab template= "split-button/vertical", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

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
        text: 'Cut',
    },
    {
        text: 'Copy',
    },
    {
        text: 'Paste',
    }];
  public render() {
    return (
    <div>
       <SplitButtonComponent cssClass= 'e-vertical' items = {this.items} iconCss= 'e-sb-icons e-paste' iconPosition='Top'>Paste</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the SplitButton using the [`iconCss`](../api/split-button#iconcss) property.

## Separator

SplitButton component has Separator support. This can be achieved by setting `separator` as `true`.

The following example illustrates how to enable separator support in SplitButton component.

{% tab template= "split-button/separator", sourceFiles="app/**/*.tsx,index.html,style.css", isDefaultActive=true, compileJsx=true %}

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
    },
    {
        separator: true
    },
    {
      iconCss: 'e-sb-icons e-font',
      text: 'Font'
    },
    {
      iconCss: 'e-sb-icons e-paragraph',
      text: 'Paragraph'
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

## See Also

* [SplitButton popup with icons](./popup-items#icons)
