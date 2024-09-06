---
title: "Set the Read-only TextBox"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Set the Read-only TextBox

You can make the TextBox as `read-only` by setting the `readonly` attribute to the input element.

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class Default extends React.Component {

public render() {
   return (
<div>
<input className="e-input" type="text" placeholder="Enter Name" value="John" readOnly= {true}/>

<div className="e-float-input">
    <input type='text' required = {true} readOnly = {true} value="John"   onFocus = {this.onInputFocus} onBlur = {this.onInputBlur}/>
    <span className="e-float-line"/>
    <label className="e-float-text e-label-top">Enter Name</label>
</div>
</div>
);
}


public onInputFocus(args: React.FocusEvent) {
    if (!((args.target as HTMLElement).parentElement as HTMLElement).classList.contains('e-input-in-wrap')) {
         ((args.target as HTMLElement).parentElement as HTMLElement).classList.add('e-input-focus');
    } else {
         (((args.target as HTMLElement).parentElement as HTMLElement).parentElement as HTMLElement).classList.add('e-input-focus')
    }
}

public onInputBlur(args: React.FocusEvent) {
    if (!((args.target as HTMLElement).parentElement as HTMLElement).classList.contains('e-input-in-wrap')) {
    ((args.target as HTMLElement).parentElement as HTMLElement).classList.remove('e-input-focus');
    } else {
        (((args.target as HTMLElement).parentElement as HTMLElement).parentElement as HTMLElement).classList.remove('e-input-focus');
    }
}
}
ReactDOM.render(<Default />, document.getElementById('input-container'));

```

{% endtab %}
