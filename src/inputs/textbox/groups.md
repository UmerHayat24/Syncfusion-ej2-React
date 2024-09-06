---
title: "Groups"
component: "Textbox"
description: "Explains how to add icons and clear button to the floating text box that is  achieved with or without the required attribute."
---

# Groups

The following section explains you the steps required to create TextBox with `icon` and `floating label`.

TextBox:

* Create a parent div element with the class `e-input-group`

* Place input element with the class `e-input` inside the parent div element.

```typescript
import * as React from "react";
import './App.css';
export default class App extends React.Component<{}, {}> {
    public render() {
      return (
        // element which is going to render the TextBox
        <input className="e-input" type="text" placeholder="Enter Name" />
      );
    }
};

```

Floating label:

* Add the `e-float-input` class to the parent div element.

* Remove the e-input class and add `required` attribute to the input element.

* Place the span element with class `e-float-line` after the input element.

* Place the label element with class `e-float-text` after the above created span element.
When you focus or filled with value in the TextBox, the label floats above the TextBox.

> Creating the Floating label TextBox, you have to set the `required` attribute to the Input element to
achieve the floating label functionality which is used for validating the value existence in TextBox.
If you want to render the Floating label TextBox without
`required` attribute then refer to the [Floating Label without required attribute](#floating-Label-without-required-attribute) section.

```typescript
import * as React from "react";
import './App.css';
export default class App extends React.Component<{}, {}> {
    public render() {
      return (
        // element which is going to render the Floating TextBox
        <div className="e-float-input e-input-group">
            <input type="text" required={true}/>
            <span className="e-float-line"/>
            <label className="e-float-text">Enter Name </label>
        </div>
      );
    }
};

```

And refer to the following sections to add the icons to the TextBox.

## With icon and floating label

Create an icon element as a span with the class `e-input-group-icon`, and the user can place
the icon in either side of TextBox by adding the created icon element before/after the input.

For the floating label enabled TextBox add the icon element as first or last element inside the TextBox wrapper,
and based on the element position it will act as prefix or suffix icon.

{% tab template="textbox/textbox-icons", sourceFiles="app/**/*.tsx,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class Default extends React.Component {

public render() {
   return (
    <div>

    <h4> TextBox with icons </h4>

    <div className="e-input-group ">
        <input className="e-input" type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} placeholder="Enter Date"/>
        <span className="e-input-group-icon e-input-popup-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
    </div>

    <div className="e-input-group e-float-icon-left">
        <span className="e-input-group-icon e-input-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
        <div className="e-input-in-wrap">
            <input className="e-input" type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} placeholder="Enter Date"/>
        </div>
    </div>

    <div className="e-input-group e-float-icon-left">
        <span className="e-input-group-icon e-input-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
        <div className="e-input-in-wrap">
            <input className="e-input" type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} placeholder="Enter Date"/>
            <span className="e-input-group-icon e-input-down"/>
        </div>
    </div>

    <h4> Floating label with icons </h4>

    <div className="e-float-input e-input-group">
        <input required = {true} type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} />
        <span className="e-float-line"/>
        <label className="e-float-text"> Enter Date </label>
        <span className="e-input-group-icon e-input-popup-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
    </div>

    <div className="e-float-input e-input-group e-float-icon-left">
        <span className="e-input-group-icon e-input-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
        <div className="e-input-in-wrap">
            <input required = {true} type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} />
            <span className="e-float-line"/>
            <label className="e-float-text"> Enter Date </label>
        </div>
    </div>

    <div className="e-float-input e-input-group e-float-icon-left">
        <span className="e-input-group-icon e-input-date" onMouseDown = {this.onIconMouseDown} onMouseUp = {this.onIconMouseUp}/>
        <div className="e-input-in-wrap">
            <input required = {true} type="text" onFocus = {this.onInputFocus} onBlur = {this.onInputBlur} />
            <span className="e-float-line"/>
            <label className="e-float-text"> Enter Date </label>
            <span className="e-input-group-icon e-input-down"/>
        </div>
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


public onIconMouseDown(args: React.MouseEvent) {
    args.persist();
    setTimeout(
        () => {
            (args.target as HTMLElement).classList.add('e-input-btn-ripple');
        },
    300);
}

public onIconMouseUp(args: React.MouseEvent) {
    (args.target as HTMLElement).classList.remove('e-input-btn-ripple');
}
}

ReactDOM.render(<Default />, document.getElementById('input-container'));

```

{% endtab %}

> To place the icon on left side of the TextBox, create a div element with the class `e-input-in-wrap` as wrapper to the input element and
place the `floating line`, `floating text`, and right side icon element within it.
Add the `e-float-icon-left` class to the TextBox container element.

## With clear button and floating label

The clear button is added to the input for clearing the value given in the TextBox.
It is shown only when the input field has a value, otherwise not shown.

You can add the clear button to the TextBox by using `showClearButton` API in textbox.

{% tab template="textbox/textbox-component-clearicon", sourceFiles="app/**/index.tsx" %}

```typescript
import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";
export default class App extends React.Component<{}, {}> {
    public render() {
        return (
              <div className="App">
                <div className="textboxes">
                    <h4>Textbox with clear button</h4>
                    <TextBoxComponent placeholder="First Name" showClearButton= {true} floatLabelType="Never"/>
                </div>
                <div className="textboxes">
                    <h4>Floating textbox with clear button</h4>
                    <TextBoxComponent placeholder="Last Name" showClearButton= {true} floatLabelType="Auto"/>
                </div>
            </div>
        )
    }
};

ReactDOM.render(<App />, document.getElementById('input-container'));

```

{% endtab %}

## Floating Label without required attribute

You can render the `Floating label TextBox` without `required` attribute by manually
float the label above of the TextBox using input events.
You can manually float the label above of the TextBox by adding the below list of
classes to the floating label element. The classes are:

Class Name        | Description
------------------| -------------
  e-label-top     | Floats the label above of the TextBox.
  e-label-bottom  | Label to be placed as placeholder for the TextBox.

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public textboxInstance: any;
    constructor(props: any) {
        super(props);
        this.onFocusOut = this.onFocusOut.bind(this);
        this.onFocusIn = this.onFocusIn.bind(this);
        this.onInputEvt = this.onInputEvt.bind(this);
    }

    public onFocusOut(args: React.FocusEvent) {
        /* Update the label position based on Input value */
        this.updateLabelState((args.target as HTMLInputElement).value, ((args.target as HTMLElement).parentElement as HTMLElement).querySelector('.e-float-text') as HTMLElement);
    }

    public onFocusIn(args: React.FocusEvent) {
        const label = ((args.target as HTMLElement).parentElement as HTMLElement).querySelector('.e-float-text') as HTMLElement;
        label.classList.add('e-label-bottom');
        label.classList.remove('e-label-top');
    }
    public onInputEvt(args: React.FormEvent) {
    /* Update the label position based on Input value */
      this.updateLabelState((args.target as HTMLInputElement).value, ((args.target as HTMLElement).parentElement as HTMLElement).querySelector('.e-float-text') as HTMLElement);
    }

    /* Update the label position based on Input value */
    public updateLabelState(value: string ,label: HTMLElement) {

    /* e-label-top - Float the label above of the Input */
    /* e-label-bottom - Move the label to the Input */

        if (value) {
            label.classList.add('e-label-top');
            label.classList.remove('e-label-bottom');
        } else {
            label.classList.add('e-label-bottom');
            label.classList.remove('e-label-top');
        }
    }

    public render() {
        return (
            <div className="inner-container">
                <h4> Floating label without required attribute </h4>
                <div className="e-float-input">
                  <input id='inpt1' type="text" onInput= {this.onInputEvt}  onFocus={this.onFocusIn} onBlur={ this.onFocusOut } ref = {e => this.textboxInstance = e!} />
                  <span className="e-float-line"/>
                  <label className="e-float-text">First Name</label>
                </div>
            </div>
        )
    }

    public componentDidMount() {
        /* Update the label position based on initial input value */
        this.updateLabelState(this.textboxInstance.value, this.textboxInstance.parentElement.querySelector('.e-float-text'));
    }
};
ReactDOM.render(<App />, document.getElementById('input-container'));

```

{% endtab %}

## Multi-line input with floating label

Add the HTML textarea element with the `e-input` class to create default multi-line input.

Add the floating label support to the `multi-line input` by creating the floating label structure as defined in the initial section.

{% tab template="textbox/default", sourceFiles="app/**/index.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
export default class App extends React.Component<{}, {}> {
    public render() {
        return (
            <div>
                <textarea className="e-input" placeholder="Address"/>
                <div className="e-float-input">
                    <textarea required={true}/>
                    <span className="e-float-line"/>
                    <label className="e-float-text"> Address</label>
                </div>
            </div>
        )
    }
};

ReactDOM.render(<App />, document.getElementById('input-container'));

```

{% endtab %}

## See Also

* [How to add floating label to TextBox programmatically](./how-to/add-floating-label-to-textbox-programmatically)
* [Change the floating label color of the TextBox](./how-to/change-the-floating-label-color-of-the-textbox)
* [Change the color of the TextBox based on its value](./how-to/change-the-color-of-the-textbox-based-on-its-value)
