---
title: "Add Floating Label to TextBox Programmatically"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Add Floating Label to TextBox Programmatically

The `Floating Label TextBox` floats label above the TextBox after focusing, or entering a value in the TextBox.

Floating label supports the types of actions as given below.

Type     | Description
------------ | -------------
  Auto       | The floating label will float above the input after focusing, or entering a value in the input.
  Always     | The floating label will always float above the input.
  Never      | By default, never float the label in the input when the placeholder is available.

* Create a TypeScript file and import the `Input` modules from `ej2-inputs` library as shown below.

```typescript
import {Input} from '@syncfusion/ej2-inputs';
```

* Pass the `HTML Input` element and `floatLabelType` property as `Auto` to the `createInput` method.

* Set the `placeholder` value to the input element via `element attribute` or pass the parameter to the `createInput` method.

The `watermark label` will be updated based on the specified `placeholder` value of the `Floating Label TextBox`.

* You can add the `icons` on the input by passing `buttons` property value with the
class name `e-input-group-icon` as parameter to the `createInput` method.

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import { Input } from  '@syncfusion/ej2-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class Default extends React.Component {
    public input1: any;
    public input2: any;
    public input3: any;
    public input4: any;

    public render() {
        return (
            <div className="inner-container">
                <h4> FloatLabelType as Auto </h4>
                <input id="input-01" type="text" ref = {ele1 => this.input1 = ele1!} />
                <h4> FloatLabelType as Always </h4>
                <input id="input-02" type="text" ref = {ele2 => this.input2 = ele2!} />
                <h4> FloatLabelType as Never </h4>
                <input id="input-03" type="text" ref = {ele3 => this.input3 = ele3!} />
                <h4> Float label input with icons </h4>
                <input id="input-04" type="text" ref = {ele4 => this.input4 = ele4!} />
            </div>
        )
    }

    public componentDidMount() {

        Input.createInput({
            element: this.input1,
            floatLabelType: "Auto",
            properties:{
                placeholder:'Enter Name'
            }
        });

        Input.createInput({
            element: this.input2,
            floatLabelType: "Always",
            properties:{
                placeholder:'Enter Name'
            }
        });

        Input.createInput({
            element: this.input3,
            floatLabelType: "Never",
            properties:{
                placeholder:'Enter Name'
            }
        });

        // Render Float Label TextBox with Icon
        Input.createInput({
            buttons: ['e-input-group-icon e-input-down'],
            element: this.input4,
            floatLabelType: "Auto",
            properties:{
                placeholder:'Enter Value'
            }
        });
    }
}

ReactDOM.render(<Default />, document.getElementById('input-container'));

```

{% endtab %}
