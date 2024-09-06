---
title: "Multiline"
component: "Textbox"
description: "Explains about multiple lines of text like address, description and feedback are allows to fill in multiline textbox and it can be editable or can copy the text."
---

# Multiline TextBox

This feature allows the textbox to accept one or more lines of text like address, description, comments, and more.

## Create multiline textbox

You can convert the default textbox into the multiline textbox by setting the [multiline](../api/textbox/#multiline) API value as true or pass HTML5 textarea as element to the textbox.

> The multiline textbox allows you to resize it in vertical direction alone.

{% tab template="textbox/textarea", sourceFiles="app/**/*.tsx" %}

```typescript

import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public render() {
      return (
        <div className="multiline">
              <TextBoxComponent multiline={true} placeholder='Enter your address' value= 'Mr. Dodsworth Dodsworth, System Analyst, Studio 103, The Business Center'/>
        </div>
      );
  }
}

ReactDOM.render(<App />, document.getElementById('default'));

```

{% endtab %}

## Implementing floating label

You can achieve the floating label behavior in the multiline textbox by setting `floatLabelType` as 'Auto'. The placeholder text act as floating label to the multiline textbox. You can provide the placeholder text to the multiline textbox either by using the `placeholder` property or placeholder attribute.

{% tab template="textbox/float", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public render() {
    return (
        <div className="multiline">
            <label className='label'>Float label type Auto</label>
            <TextBoxComponent multiline={true} placeholder='Enter your address' floatLabelType='Auto'/>
            <label className='label'>Float label type Always</label>
            <TextBoxComponent multiline={true} placeholder='Enter your address' floatLabelType='Always'/>
            <label className='label'>Float label type Never</label>
            <TextBoxComponent multiline={true} placeholder='Enter your address' floatLabelType='Never'/>
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('default'));

```

{% endtab %}

## Auto resizing

By default, you can manually resize the multiline textbox. But you can also create an `auto resizing` multiline textbox with both the initial and dynamic value change. It can be done by calculating the height of the textarea in the created event for initial value update and in the input event for dynamic value update of the auto resize multiline textbox, as explained in the following code sample.

{% tab template="textbox/resize", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
 public  textareaObj: any;
  public render() {
    return (
        <div className="multiline">
        <TextBoxComponent multiline={true} value= 'Mr. Dodsworth Dodsworth, System Analyst, Studio 103, The Business Center' input={this.onInput = this.onInput.bind(this)} created={this.onCreate = this.onCreate.bind(this)} placeholder='Enter your address' floatLabelType='Auto' ref = {scope => {this.textareaObj = scope }}/>
        </div>
    );
  }
    private onCreate(): void {
        this.textareaObj.addAttributes({rows: 1});
        this.textareaObj.respectiveElement.style.height = "auto";
        this.textareaObj.respectiveElement.style.height = (this.textareaObj.respectiveElement .scrollHeight)+"px";
    }
    private onInput(): void {
        this.textareaObj.respectiveElement.style.height = "auto";
        this.textareaObj.respectiveElement.style.height = (this.textareaObj.respectiveElement .scrollHeight)+"px";
    }
}

ReactDOM.render(<App />, document.getElementById('default'));

```

{% endtab %}

## Disable resizing

By default, the multiline textbox is rendered with resizable. You can disable the resize of the multiline textbox by applying the following CSS styles.

```CSS
    textarea.e-input,
    .e-float-input textarea,
    .e-float-input.e-control-wrapper textarea,
    .e-input-group textarea,
    .e-input-group.e-control-wrapper textarea {
        resize: none;
    }

```

{% tab template="textbox/disable", sourceFiles="app/**/*.tsx,index.html" %}

```typescript


import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div className="multiline">
            <TextBoxComponent name="disable" multiline={true} placeholder='Enter your address' floatLabelType='Auto' cssClass="sample"/>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('default'));

```

{% endtab %}

## Limit the text length

By default, the text length of the multiline textbox is unlimited. You can limit the text length by setting the `maxLength` attribute using the `addAttribute` method.

{% tab template="textbox/length", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public textareaObj: any;
  public render() {
    return (
      <div className="multiline">
            <label className="label">Add maxlength attribute through inline</label>
             <TextBoxComponent multiline={true} maxlength={'15'} placeholder='Enter your address' floatLabelType='Auto'/>
             <label className="label">Add maxlength attribute through addAttributes method</label>
            <TextBoxComponent multiline={true} ref = {scope => {this.textareaObj = scope }} placeholder='Enter your address' floatLabelType='Auto'/>
            <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)} >Add max length</button>
      </div>
    );
     }
    private handleClick(): void {
        this.textareaObj.addAttributes({maxlength: 15});
    }
}

ReactDOM.render(<App />, document.getElementById('default'));

```

{% endtab %}

## Count characters

You can show the number of characters entered inside the textarea by calculating the character count in the input event of multiline textbox. The character count is updated while entering or deleting any character inside the textarea. The character count shows how many characters can be entered or left to be entered.

{% tab template="textbox/count", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public textareaObj: any;
  public render() {
    return (
      <div className="multiline">
            <TextBoxComponent multiline={true}  input={this.onInput = this.onInput.bind(this)} placeholder='Enter your address' floatLabelType='Auto' maxlength='25' ref = {scope => {this.textareaObj = scope }}/>
            <span id='numbercount'/>
      </div>
    );
  }

    private onInput(): void {
        let word: string;
        let addressCount: number;
        word = this.textareaObj.respectiveElement.value;
        addressCount = word.length;
        (document.getElementById('numbercount') as HTMLElement).textContent = addressCount+"/25";
    }
}

ReactDOM.render(<App />, document.getElementById('default'));

```

{% endtab %}
