---
title: "Customized CheckBox"
component: "CheckBox"
description: "React CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Customized CheckBox

## Customize CheckBox Appearance

You can customize the appearance of the CheckBox component using the CSS rules.
Define own CSS rules according to your requirement and assign the class name to the [`cssClass`](../../api/check-box#cssclass) property.

The background and border color of the CheckBox is customized through custom classes to create primary, success, warning, danger, and
info type of checkbox.

{% tab template="check-box/howto", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// To customize CheckBox appearance.
class App extends React.Component<{}, {}> {
  public render() {
    return (
        <ul>
            {/* Refer the 'e-primary' class details in 'style.css'.*/}
            <li><CheckBoxComponent label="Primary" cssClass="e-primary" checked={true} /></li>

            {/* Refer the 'e-success' class details in 'style.css'.*/}
            <li><CheckBoxComponent label="Success" cssClass="e-success" checked={true} /></li>

            {/* Refer the 'e-info' class details in 'style.css'.*/}
            <li><CheckBoxComponent label="Info" cssClass="e-info" checked={true} /></li>

            {/* Refer the 'e-warning' class details in 'style.css'.*/}
            <li><CheckBoxComponent label="Warning" cssClass="e-warning" checked={true} /></li>

            {/* Refer the 'e-danger' class details in 'style.css'.*/}
            <li><CheckBoxComponent label="Danger" cssClass="e-danger" checked={true} /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}

## Custom Frame

CheckBox frame can be customized as per the requirement by adding CSS rules.

In the following example, to-do list is displayed with round checkbox by changing
`border-radius` as `100%` by adding `e-custom` class.

{% tab template="check-box/custom-frame", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);
// To customize CheckBox appearance.
class App extends React.Component<{}, {}> {
  public render() {
    return (
        <ul>
            <li><CheckBoxComponent label="Buy Groceries" cssClass="e-custom" checked={true} /></li>

            <li><CheckBoxComponent label="Pay Rent" cssClass="e-custom" /></li>

            <li><CheckBoxComponent label="Make Dinner" cssClass="e-custom" /></li>

            <li><CheckBoxComponent label="Finish To-do List Article" cssClass="e-custom" /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}

## Custom Check Icon

CheckBox check icon can be customized as per the requirement by adding CSS rules.

In the following example, the check icon can be customized by changing check icon content, background and
border color in focus and hovered states by adding `e-checkicon` class.

{% tab template="check-box/custom-frame", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);
// To customize CheckBox appearance.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ul>
            <li><CheckBoxComponent label="Buy Groceries" cssClass="e-checkicon" checked={true} /></li>

            <li><CheckBoxComponent label="Pay Rent" cssClass="e-checkicon" /></li>

            <li><CheckBoxComponent label="Make Dinner" cssClass="e-checkicon" /></li>

            <li><CheckBoxComponent label="Finish To-do List Article" cssClass="e-checkicon" /></li>
        </ul>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}