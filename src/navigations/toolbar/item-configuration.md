---
title: "Toolbar Item configuration"
component: "Toolbar"
description: "Toolbar items are constructed with built-in command types or item templates such as separator, button, and input."
---

# Item Configuration

The Toolbar can be rendered by defining an array of [`items`](../api/toolbar#items). Items can be constructed with the following built-in command types or item template.

## Button

`Button` is the default command [`type`](../api/toolbar/item#type), and it can be rendered by using the [`text`](../api/toolbar/item#text) property.
Properties of the button command type:

  Property   | Description
------------ | -------------
  [`text`](../api/toolbar/item#text) | The text to be displayed for button.
 [`id`](../api/toolbar/item#id) | The ID of the button to be rendered. If the ID is not given, auto ID is generated.
  [`prefixIcon`](../api/toolbar/item#prefixicon) | Defines the class used to specify an icon for the button. The icon is `positioned before` the text if text is available or the icon alone button is rendered.
[`suffixIcon`](../api/toolbar/item#suffixicon) | Defines the class used to specify an icon for the button. The icon is `positioned after` the text if text is available. If both [`prefixIcon`](../api/toolbar/item#prefixicon) and [`suffixIcon`](../api/toolbar/item#suffixicon) are specified, only `prefixIcon` is considered.
  [`width`](../api/toolbar/item#width) | Used to set the [`width`](../api/toolbar/item#width) of the button.
  [`align`](../api/toolbar/item#align) | Specifies the location for aligning Toolbar items.

## Separator

The `Separator` type adds a vertical separation between the Toolbar single/multiple commands.

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
          <ItemDirective text="Cut" />
          <ItemDirective text="Copy" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Paste" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Undo" />
          <ItemDirective text="Redo" />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

> If `Separator` is added as first or last item, it is not visible.

## Input

The `Input` type is only applicable for adding `template` elements when the [`template`](../api/toolbar/item#template) property is defined as an `object`.
Input type creates an `input element` internally that acts as the container for `Syncfusion` input based components.

### NumericTextBox

 E.g. The following code explains about how to add `NumericTextBox` component to the Toolbar.

* The `NumericTextBox` component can be included by importing the `NumericTextBox` module from `ej2-inputs`.

* Initialize the `NumericTextBox` in template property, in which the Toolbar item type set as `Input`.

* Related `NumericTextBox` component properties are also can be configured like as below.

```javascript
new NumericTextBox( { format: 'c2' }))
```

### DropDownList

 E.g. The following code explains about how to add `DropDownList` component to the Toolbar.

* The `DropDownList` component can be included by importing the `DropDownList` module from `ej2-dropdowns`.

* Initialize the `DropDownList` in template property, in which the Toolbar item type set as `Input`.

* Related `DropDownList` component properties are also can be configured like as below.

```javascript
new DropDownList({ width:100 })
```

### CheckBox

 E.g. The following code explains about how to add `CheckBox` component to the Toolbar.

* The `CheckBox` component can be included by importing the `CheckBox` module from `ej2-buttons`.

* Initialize the `CheckBox` in template property, in which the Toolbar item type set as `Input`.

* Related `CheckBox` component properties are also can be configured like as below.

```javascript
new CheckBox({ label: 'Checkbox', checked: true })
```

### RadioButton

 E.g. The following code explains about how to add `RadioButton` component to the Toolbar.

* The `RadioButton` component can be included by importing the `RadioButton` module from `ej2-buttons`.

* Initialize the `RadioButton` in template property, in which the Toolbar item type set as `Input`.

* Related `RadioButton` component properties are also can be configured like as below.

```javascript
new RadioButton({ label: 'Radio', name: 'default', checked: true })
```

Above steps applicable for all 'Syncfusion' input based components.

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import { CheckBox, RadioButton } from '@syncfusion/ej2-buttons';
import { DropDownList} from '@syncfusion/ej2-dropdowns';
import { NumericTextBox} from '@syncfusion/ej2-inputs';
import { ItemDirective, ItemsDirective, ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public data: any = ['Badminton', 'Basketball', 'Cricket', 'Golf', 'Hockey', 'Rugby'];
  public numericTem: any = new NumericTextBox({ format: 'c2', value:1 });
  public templateDropdown: any = new DropDownList({ dataSource: this.data, width: 120, index: 2 });
  public templateCheckbox: any = new CheckBox({ label: 'Checkbox', checked: true });
  public templateRadiobutton: any = new RadioButton({ label: 'Radio', name: 'default', checked: true });

  public render() {
    return (
      <ToolbarComponent >
        <ItemsDirective>
          <ItemDirective text="Cut" />
          <ItemDirective text="Copy" />
          <ItemDirective type="Separator" />
          <ItemDirective text="Undo" />
          <ItemDirective text="Redo" />
          <ItemDirective type="Separator" />
          <ItemDirective type="Input" template={this.numericTem} />
          <ItemDirective type="Input" template={this.templateDropdown} />
          <ItemDirective type="Input" template={this.templateCheckbox} />
          <ItemDirective type="Input" template={this.templateRadiobutton} />
        </ItemsDirective>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

## See Also

* [How to set item wise custom template](./how-to/set-item-wise-custom-template/)
