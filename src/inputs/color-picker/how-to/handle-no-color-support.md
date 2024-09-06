---
title: "No Color support in ColorPicker"
component: "ColorPicker"
description: "This section explains, how to add no color support in ColorPicker"
---

# Handle no color support

The ColorPicker component supports no color functionality. By clicking the no color tile from palette, the selected color becomes `empty` and considered as no color has been selected from color picker.

## Default no color

To achieve this, set [`noColor`](../../api/color-picker#nocolor) property as `true`.

In the following sample, the first tile of the color palette represents the no color tile. By clicking the no color tile you can achieve the above functionalities.

{% tab template="colorpicker/no-color/default", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent, ColorPickerEventArgs } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    public preview: HTMLElement;
    constructor(props: any) {
        super(props);
        this.onChange = this.onChange.bind(this);
    }
    public onChange (args: ColorPickerEventArgs): void {
        this.preview.style.backgroundColor = args.currentValue.hex;
        this.preview.textContent = args.currentValue.hex ? args.currentValue.hex : 'No color';
    }

    public componentDidMount() {
        this.preview = document.getElementById('preview') as HTMLElement;
        this.preview.style.backgroundColor = '#ba68c8';
        this.preview.textContent = '#ba68c8';
    }

    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <div id='preview'/>
                <h4>Select Color</h4>
                <ColorPickerComponent id='colorpicker' value='#ba68c8' mode='Palette' noColor={true} showButtons={false} modeSwitcher={false} change={this.onChange}/>
            </div>
          </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

<!-- markdownlint-disable -->
<!-- ## Custom no color

The following sample show the color palette with custom no color option.

{% tab template="colorpicker/no-color/custom", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ColorPickerComponent, PaletteTileEventArgs, ColorPickerEventArgs } from '@syncfusion/ej2-react-inputs';
import { SplitButtonComponent } from '@syncfusion/ej2-react-splitbuttons';

class App extends React.Component<{}, {}> {
    public preview: HTMLElement;
    public splitBtn: SplitButtonComponent;
    public colorPicker: ColorPickerComponent;

    public presets: { [key: string]: string[] } = {
        'custom': ['#f44336', '#e91e63', '#9c27b0', '#673ab7', '#2196f3', '#03a9f4', '#00bcd4', '#009688', '#8bc34a', '#cddc39', '#ffeb3b', '#ffc107']
    };

    public beforeTileRender(args: PaletteTileEventArgs): void {
        args.element.classList.add('e-custom-tile');
    }

    public onChange (args: ColorPickerEventArgs): void {
        (document.querySelector(".e-split-btn .e-picker-icon") as HTMLElement).style.borderBottomColor = args.currentValue.hex;
        this.preview.style.backgroundColor = args.currentValue.hex;
        this.preview.textContent = args.currentValue.hex;
        if (this.splitBtn.element.getAttribute("aria-expanded")) {
            this.splitBtn.toggle();
            this.splitBtn.element.focus();
        }
    }

    public onCreated() {
        this.preview = document.getElementById('preview');
        this.preview.style.backgroundColor = '#ba68c8';
        this.preview.textContent = '#ba68c8';
        let proxy: any = this;
        document.getElementById('no-color').onclick = (): void => {
            //sets color picker value property to null
            proxy.setProperties({ 'value': '' }, true);
            (document.querySelector('.e-split-btn .e-picker-icon') as HTMLElement).style.borderBottomColor = 'transparent';
            proxy.preview.textContent = 'No color';
            proxy.preview.style.backgroundColor = 'transparent';
        }
    }

    render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <ul id="target" tabindex="0">
                    <li className="e-item e-palette-item">
                        <ColorPickerComponent id='colorpicker' value='#f44336' mode='Palette' inline={true} columns={4} presetColors={this.presets} showButtons={false} modeSwitcher={false} beforeTileRender={this.beforeTileRender} change={this.onChange.bind(this)} created={this.onCreated}></ColorPickerComponent>
                    </li>
                    <li className="e-item" id="no-color" tabindex="-1">
                        <span className="e-menu-icon e-nocolor"></span>
                        No color
                    </li>
                </ul>
                <div>
                    <div id='preview'></div>
                    <h4>Select color</h4>
                    <SplitButtonComponent id='splitbtn' iconCss='e-cp-icons e-picker-icon' target='#target' ref={(scope) => { this.splitBtn = scope; }}></SplitButtonComponent>
                </div>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %} -->