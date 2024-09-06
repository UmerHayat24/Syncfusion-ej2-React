---
title: "Place ColorPicker in Dropdownbutton"
component: "ColorPicker"
description: "This section explains, how to place the ColorPicker inside the Dropdown button."
---

# ColorPicker in DropDownButton

This section explains about how to render the ColorPicker in DropDownButton. The
[`target`](../../api/drop-down-button#target) property of the DropDownButton helps to achieve this scenario. To know about the usage of `target` property refer to [`Popup templating`](./../../drop-down-button/popup-items#popup-templating) section.

In the below sample, the color picker is rendered as inline type by setting [`inline`](../../api/color-picker#inline) property as `true` and the rendered color picker wrapper is passed as a `target` to the DropDownButton to achieve the above scenario.

{% tab template="colorpicker/dropdownbtn", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent, ColorPickerEventArgs } from '@syncfusion/ej2-react-inputs';
import { DropDownButtonComponent} from '@syncfusion/ej2-react-splitbuttons';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    public ddb: DropDownButtonComponent;
    public cp: ColorPickerComponent;
    constructor(props: any) {
        super(props);
        this.onChange = this.onChange.bind(this);
        this.onCreated = this.onCreated.bind(this);
    }
    public onChange(args: ColorPickerEventArgs): void {
        (this.ddb.element.children[0] as HTMLElement).style.backgroundColor = args.currentValue.rgba;
        this.closePopup();
    }  

    public closePopup(): void {
        this.ddb.toggle();
    }

    public onCreated() {
        const parentElem = this.cp.element.parentElement as HTMLElement;
        const cancelBtn = parentElem.querySelector('.e-cancel') as HTMLElement;
        cancelBtn.addEventListener('click', this.closePopup.bind(this));
    }

    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent ref={(scope) => { this.cp = scope as ColorPickerComponent; }} id='colorpicker' inline={true} change={this.onChange}/>
                <DropDownButtonComponent id='dropdownbtn' target='.e-colorpicker-wrapper' ref={(scope) => { this.ddb = scope as DropDownButtonComponent; }} iconCss='e-dropdownbtn-preview' created={this.onCreated}/>
            </div>
          </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
