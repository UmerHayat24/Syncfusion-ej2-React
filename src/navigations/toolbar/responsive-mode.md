---
title: "Toolbar Responsive"
component: "Toolbar"
description: "Toolbar has responsive support to adapt toolbar control width based on the devices like mobile and tablet."
---

# Responsive Mode

This section explains the supported display modes of the Toolbar when the content exceeds the viewing area. Possible modes are:

* Scrollable
* Popup

## Scrollable

The default overflow mode of the Toolbar is `Scrollable`. Scrollable display mode supports display of commands in a single line with
horizontal scrolling enabled when commands overflow to available space.

* The right and left navigation arrows are added to the start and end of the Toolbar to navigate to hidden commands.
* You can also see the hidden commands using touch swipe action.
* By default, if navigation icon in the `left` side is disabled, you can see the hidden commands by moving to the `right`.
* By clicking the arrow or by holding the arrow continuously,  hidden commands will become visible.
* If device navigation icons are not available, you can touch swipe to see the hidden commands of the Toolbar.

![Scrollable](images/scrolling.gif)

* Once the Toolbar reaches the last or first command, the  corresponding navigation icon will be disabled and you can move to the opposite direction.

![Touch scroll](images/scrolling_touch.gif)

![Swipe scroll](images/scrolling_swipe.gif)

* You can continuously scroll the Toolbar content by holding the navigation icon.

![Long press scroll](images/scrolling_long_press.gif)

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent >
        <ItemsDirective>
          <ItemDirective text="Cut" prefixIcon="e-cut-icon tb-icons" />
          <ItemDirective text="Copy" prefixIcon="e-copy-icon tb-icons" />
          <ItemDirective text="Paste" prefixIcon="e-paste-icon" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Bold" prefixIcon="e-bold-icon tb-icons" />
          <ItemDirective text="Underline" prefixIcon="e-underline-icon tb-icons" />
          <ItemDirective text="Italic" prefixIcon="e-italic-icon tb-icons" />
          <ItemDirective text="Color-Picker" prefixIcon="e-color-icon tb-icons" />
          <ItemDirective type="Separator" />
          <ItemDirective text="A-Z Sort" prefixIcon="e-ascending-icon tb-icons" />
          <ItemDirective text="Z-A Sort" prefixIcon="e-descending-icon tb-icons" />
          <ItemDirective text="Clear" prefixIcon="e-clear-icon tb-icons" />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

## Popup

`Popup` is another type of [`overflowMode`](../api/toolbar#overflowmode) in which the Toolbar container holds the commands that can be placed in the available
space. The rest of the overflowing commands that do not fit within
the viewing area moves to the overflow popup container.

The commands placed in the popup can be viewed by opening the popup using the drop down icon given at the end of the Toolbar.

![Toolbar popup](images/popup.gif)

> If the popup content overflows the height of the page, then the rest of the commands will be hidden.

### Priority of commands

Default popup priority is set as `none` and when the commands of Toolbar overflows,
the ones that are listed at last in it will be moved into the popup.

User can customize the priority of commands to be displayed in the Toolbar and popup by using the [`overflow`](../api/toolbar/itemModel#overflow) property.
Possible options:

Property     | Description
------------ | -------------
  show       | Always shows item in the `Toolbar with primary` priority.
  hide       | Always shows item in `popup with secondary` priority.
  none       | No priority considers to display and as per the `normal order` commands are moves to popup when content exceeds viewing area.

If primary priority commands are also exceeds from available space, then those are moved to the popup container at top order
position and placed before the secondary priority commands.

> You can maintain toolbar item on popup always by using the [`showAlwaysInPopup`](../api/toolbar/item#showalwaysinpopup) property, and this behavior is not applicable for toolbar items with [`overflow`](../api/toolbar/item#overflow) property as 'show'.

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent width="380" overflowMode="Popup">
        <ItemsDirective>
          <ItemDirective text="Cut" prefixIcon="e-cut-icon tb-icons" overflow="Show" />
          <ItemDirective text="Copy" prefixIcon="e-copy-icon tb-icons" overflow="Show" />
          <ItemDirective text="Paste" prefixIcon="e-paste-icon" overflow="Show" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Bold" prefixIcon="e-bold-icon tb-icons" />
          <ItemDirective text="Underline" prefixIcon="e-underline-icon tb-icons" />
          <ItemDirective text="Italic" prefixIcon="e-italic-icon tb-icons" />
          <ItemDirective type="Separator" />
          <ItemDirective text="A-Z Sort" prefixIcon="e-ascending-icon tb-icons" overflow="Show" />
          <ItemDirective text="Z-A Sort" prefixIcon="e-descending-icon tb-icons" overflow="Show" />
          <ItemDirective text="Clear" prefixIcon="e-clear-icon tb-icons" />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

### Text mode for buttons

The [`showTextOn`](../api/toolbar/item#showtexton) property is used to decide the button text display area in the Toolbar, popup or in both places.
This is useful to do customization in which the user needs to show the text and image representation of commands.

For example, the user can show icon only button in the Toolbar and where in a popup
container user can show more information about the commands with icon and text.

Possible values are,

  Property   | Description
------------ | -------------
  Both     | Button Text is visible in both `Toolbar` and `Popup`.
  Overflow | Button Text is only visible in `Popup`.
  Toolbar  | Button Text is only visible in the `Toolbar`.

In below sample text only visible at popup container not in the Toolbar container.

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent width="330" overflowMode="Popup">
        <ItemsDirective>
          <ItemDirective text="Cut" prefixIcon="e-cut-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Copy" prefixIcon="e-copy-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Paste" prefixIcon="e-paste-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Bold" prefixIcon="e-bold-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Underline" prefixIcon="e-underline-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Italic" prefixIcon="e-italic-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Color-Picker" prefixIcon="e-color-icon tb-icons" showTextOn="Overflow" overflow="Hide" />
          <ItemDirective type="Separator" />
          <ItemDirective text="A-Z Sort" prefixIcon="e-ascending-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Z-A Sort" prefixIcon="e-descending-icon tb-icons" showTextOn="Overflow" overflow="Show" />
          <ItemDirective text="Clear" prefixIcon="e-clear-icon tb-icons" showTextOn="Overflow" overflow="Hide" />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}
