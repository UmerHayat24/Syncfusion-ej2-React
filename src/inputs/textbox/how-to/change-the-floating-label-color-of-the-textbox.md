---
title: "Change the floating label color of the TextBox"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Change the floating label color of the TextBox

You can change the floating label color of the TextBox for both `success` and `warning` validation states by applying the following CSS styles.

```CSS

    /* For Success state */
    .e-float-input.e-success label.e-float-text,
    .e-float-input.e-success input:focus ~ label.e-float-text,
    .e-float-input.e-success input:valid ~ label.e-float-text {
      color: #22b24b;
    }

    /* For Warning state */
    .e-float-input.e-warning label.e-float-text,
    .e-float-input.e-warning input:focus ~ label.e-float-text,
   .e-float-input.e-warning input:valid ~ label.e-float-text {
      color: #ffca1c;
    }

```

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class Default extends React.Component {

public render() {
   return (
    <div>
        <div className="e-float-input e-input-group e-success">
            <input type='text' required = {true} onFocus = {this.onInputFocus} onBlur = {this.onInputBlur}/>
            <span className="e-float-line"/>
            <label className="e-float-text">Success</label>
        </div>

        <div className="e-float-input e-input-group e-warning">
            <input type='text' required = {true} onFocus = {this.onInputFocus} onBlur = {this.onInputBlur}/>
            <span className="e-float-line"/>
            <label className="e-float-text">Warning</label>
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
