---
title: "RadioButton How To sections"
component: "RadioButton"
description: "React RadioButton how to section, name and value in form submit, customize RadioButton appearance."
---

# Set the disabled state

RadioButton component can be enabled/disabled by giving [`disabled`](../../api/radio-button#disabled) property. To disable RadioButton component,
the `disabled` property can be set as `true`.

The following example illustrates how to disable a radio button and the selected one is displayed using [`change`](../../api/radio-button#change) event.

{% tab template="radio-button/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { RadioButtonComponent, ChangeEventArgs } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render RadioButton.
class App extends React.Component<{}, {}> {
    public radioInstance1: RadioButtonComponent;
    public radioInstance2: RadioButtonComponent;
    public radioInstance3: RadioButtonComponent;
    public changeOption1: any = () => {
      (document.getElementById('text') as HTMLElement).innerText = 'Selected : ' + this.radioInstance1.label;
    }
  
    public changeOption2: any = () => {
        (document.getElementById('text') as HTMLElement).innerText = 'Selected : ' + this.radioInstance2.label;
    }
  
    public changeOption3: any = () => {
        (document.getElementById('text') as HTMLElement).innerText = 'Selected : ' + this.radioInstance3.label;
    }
  
    public render() {
      return (
        <ul>
        <li><div id="text">Selected : Option 1</div></li>
        <li><RadioButtonComponent label="Option 1" name="default"  checked={true} change={this.changeOption1} ref={radio1 => this.radioInstance1 = radio1 as RadioButtonComponent}/></li>
        <li><RadioButtonComponent label="Option 2" name="default" disabled={true} change={this.changeOption2} ref={radio2 => this.radioInstance2 = radio2 as RadioButtonComponent}/></li>
        <li><RadioButtonComponent label="Option 3" name="default" change={this.changeOption3} ref={radio3 => this.radioInstance3 = radio3 as RadioButtonComponent}/></li>
        </ul>
      );
    }
  }
ReactDom.render(<App />, document.getElementById('radio-button'));
```

{% endtab %}