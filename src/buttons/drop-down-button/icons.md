---
title: "DropDownButton Icons"
component: "DropDownButton"
description: "React DropDownButton allows the end user to place the icons/sprite images in DropDownButton."
---

# Icons

## DropDownButton icons

DropDownButton can have an icon to provide the visual representation of the action. To place the
icon on a DropDownButton, set the [`iconCss`](../api/drop-down-button#iconcss) property
to `e-icons` with the required icon CSS. By default, the icon is positioned to the left side of the DropDownButton. You
can customize the icon's position by using the [`iconPosition`](../api/drop-down-button#iconposition)property.

In the following example, the DropDownButton with default iconPosition and iconPosition as `Top` is showcased.

{% tab template= "drop-down-button/icon", sourceFiles="app/**/*.tsx,index.html,styles.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Edit',
    },
    {
        text: 'Delete',
    },
    {
        text: 'Mark as Read',
    },
    {
        text: 'Like Message',
    }];
  public render() {
    return (
      <div>
        <DropDownButtonComponent items = {this.items}  iconCss='ddb-icons e-message'> Message </DropDownButtonComponent>
        <DropDownButtonComponent items = {this.items}  iconCss='ddb-icons e-message' iconPosition = 'Top'> Message </DropDownButtonComponent>
         </div>
      );
    }
  }
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

### Icon only DropDownButton

Icon only DropDownButton can be achieved by using [`iconCss`](../api/drop-down-button#iconcss) property and to hide drop down arrow
`e-caret-hide` class is added using [`cssClass`](../api/drop-down-button#cssclass) property.

{% tab template= "drop-down-button/icon-only", sourceFiles="app/**/*.tsx,index.html,styles.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'New tab'
    },
    {
        text: 'New window'
    },
    {
        text: 'New incognito window'
    },
    {
        separator: true
    },
    {
        text: 'Print'
    },
    {
        text: 'Cast'
    },
    {
        text: 'Find'
    }];

  public render() {
    return (
      <div>
        <DropDownButtonComponent items = {this.items} iconCss='e-icons e-menu' cssClass= 'e-caret-hide'></DropDownButtonComponent>
      </div>
    );
  }
}

ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

### DropDownButton with sprite image

Sprite images can be loaded in DropDownButton instead of font icons using [`iconCss`](../api/drop-down-button#iconcss) property.

In this following example, `e-image` class is added with background url of the sprite image along with X and Y positions. The `width` and
`height` of the element set as `32px`.

{% tab template= "drop-down-button/sprite", sourceFiles="app/**/*.tsx,index.html,styles.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Display Settings'
    },
    {
        text: 'System Settings'
    },
    {
        text: 'Additional Settings'
    }];

  public render() {
    return (
      <div>
        <DropDownButtonComponent items = {this.items} iconCss='e-icons e-image' cssClass= 'e-caret-hide'/>
      </div>
    );
  }
}

ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the DropDownButton using the [`iconCss`](../api/drop-down-button#iconcss) property.

## Vertical button

Vertical Button in DropDownButton can be achieved by adding `e-vertical` class using `cssClass` property.

{% tab template= "drop-down-button/vertical", sourceFiles="app/**/*.tsx,index.html,styles.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Edit'
    },
    {
        text: 'Delete'
    },
    {
        text: 'Mark as Read'
    },
    {
        text: 'Like Message'
    }];

  public render() {
    return (
    <div>
      <DropDownButtonComponent items = {this.items} iconCss='ddb-icons e-message' cssClass= 'e-vertical' iconPosition='Top'> Message </DropDownButtonComponent>
      </div>
    );
  }
}

ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the DropDownButton using the [`iconCss`](../api/drop-down-button#iconcss) property.

## See Also

* [Dropdown popup with icons](./popup-items#icons)
* [Customized icon size](./how-to/customize-icon-and-width)