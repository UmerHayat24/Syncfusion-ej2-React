---
title: "Add TextBox Programmatically"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Add TextBox Programmatically

* Create a TypeScript file and import the `Input` modules
from `ej2-inputs` library as shown below.

```typescript
import {Input} from '@syncfusion/ej2-inputs';
```

* Pass the `HTML Input` element as parameter to the `createInput` method.

* You can also add the `icons` on the input by passing `buttons` property value with the class
name `e-input-group-icon` as parameter to the `createInput` method.

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import { Input } from  '@syncfusion/ej2-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class Default extends React.Component {
    public input1: any;
    public input2: any;
    public render() {
        return (
            <div className="inner-container">
                <input id="input-01" type="text" ref = { e1 => this.input1 = e1!} />
                <input id="input-02" type="text" ref = { e2 => this.input2 = e2!} />
            </div>
        )
    }

    public componentDidMount() {

        Input.createInput({
            element: this.input1,
            properties:{
                placeholder:'Enter Name'
            }
        });

        Input.createInput({
            buttons: ['e-input-group-icon e-input-down'],
            element: this.input2,
            properties:{
                placeholder:'Enter Value'
            }
        });
    }
}
ReactDOM.render(<Default />, document.getElementById('input-container'));

```

{% endtab %}