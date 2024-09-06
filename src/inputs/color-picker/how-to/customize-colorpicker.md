---
title: "Customize ColorPicker"
component: "ColorPicker"
description: "This section explains, how to customize the ColorPicker"
---

# Customize ColorPicker

## Custom palette

By default, the Palette will be rendered with default colors. To load custom colors in the palette, specify the colors in the [`presetColors`](../../api/color-picker#presetcolors) property. To customize the color palette, add a custom class to palette tiles using [`BeforeTileRender`](../../api/color-picker#beforetilerender) event.

The following sample demonstrates the above functionalities.

{% tab template="colorpicker/custom/palette", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent, ColorPickerEventArgs, PaletteTileEventArgs } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    public presets: { [key: string]: string[] } = {
        'custom1': ['#ef9a9a', '#e57373', '#ef5350',
                        '#f44336', '#f48fb1', '#f06292',
                        '#ec407a', '#e91e63', '#ce93d8',
                        '#ba68c8', '#ab47bc', '#9c27b0',
                        '#b39ddb', '#9575cd', '#7e57c2', '#673AB7'],
        'custom2': ['#9FA8DA', '#7986CB', '#5C6BC0', '#3F51B5',
                        '#90CAF9', '#64B5F6', '#42A5F5', '#2196F3',
                        '#81D4FA', '#4FC3F7', '#29B6F6', '#03A9F4',
                        '#80DEEA', '#4DD0E1', '#26C6DA', '#00BCD4'],
        'custom3': ['#80CBC4', '#4DB6AC', '#26A69A', '#009688',
                        '#A5D6A7', '#81C784', '#66BB6A', '#4CAF50',
                        '#C5E1A5', '#AED581', '#9CCC65', '#8BC34A', '#E6EE9C',
                        '#DCE775', '#D4E157', '#CDDC39']
    };

    // Triggers before rendering each palette tile.
    public tileRender(args: PaletteTileEventArgs): void {
        args.element.classList.add("e-icons");
        args.element.classList.add("e-custom-tile");
    }

    // riggers while selecting colors from palette.
    public change(args: ColorPickerEventArgs): void {
        (document.getElementById('preview') as HTMLElement).style.backgroundColor = args.currentValue.hex;
    }

    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <div id="preview"/>
                <h4>Select Color</h4>
                <ColorPickerComponent id='element' mode='Palette' modeSwitcher={false} inline={true} showButtons={false} columns={4} presetColors={this.presets} beforeTileRender={this.tileRender} change ={this.change}/>
            </div>
          </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Hide input area from picker

By default, the input area will be rendered in ColorPicker. To hide the input area from it, add `e-hide-value` class to ColorPicker using the [`cssClass`](../../api/color-picker#cssclass) property.

In the following sample, the ColorPicker is rendered without input area.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// To hide the input area
class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent cssClass="e-hide-value" modeSwitcher={false} />
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Custom handle

Color picker handle shape and UI can be customized. Here, we have customized the handle as `svg icon`. The same way you can customize the handle based on your requirement.

The following sample show the customized color picker handle.

{% tab template="colorpicker/custom/handle", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent id='colorpicker' value='#344aae' cssClass='e-custom-picker' modeSwitcher={false}/>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Custom primary button

By default, the applied color will be updated in primary button of the color picker. You can customize that as `icon`.

In the following sample, the `picker` icon is added to primary button and using [`change`](../../api/color-picker#change) event the selected color will be updated in bottom portion of the icon.

{% tab template="colorpicker/icon", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { addClass } from '@syncfusion/ej2-base';
import { ColorPickerComponent, ColorPickerEventArgs } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";
class App extends React.Component<{}, {}> {
    public previewIcon: HTMLElement;
    public cp: ColorPickerComponent;
    constructor(props: any) {
        super(props);
        this.onCreated = this.onCreated.bind(this);
        this.onChange = this.onChange.bind(this);
    }
    public onChange (args: ColorPickerEventArgs): void {
        this.previewIcon.style.borderBottomColor = args.currentValue.rgba;
    }

    public onCreated() {
        const elem = this.cp.element.nextElementSibling as HTMLElement;
        this.previewIcon = elem.querySelector('.e-selected-color') as HTMLElement;
        addClass([this.previewIcon], 'e-icons');
    }

    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent ref= {(scope) => this.cp = scope as ColorPickerComponent} id='colorpicker' created={this.onCreated} change={this.onChange}/>
            </div>
          </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

>> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element. You can also use third party icon to customize the primary button.

## Display hex code in input

The color picker input element can be showcased in the place of primary button. The applied color hex code will be updated in the primary button input.

The following sample shows the color picker with input.

{% tab template="colorpicker/input", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    public colorPicker: ColorPickerComponent;
    constructor(props: any) {
        super(props);
        this.onCreated = this.onCreated.bind(this);
    }
    public onCreated(): void {
        const cpElem = this.colorPicker.element.nextElementSibling as HTMLElement;
        cpElem.insertBefore(this.colorPicker.element, cpElem.children[1]);
    }

    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent ref={(scope) => this.colorPicker = scope as ColorPickerComponent} id='colorpicker' type='text' created={this.onCreated} className='e-input'/>
            </div>
          </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

<!-- markdownlint-disable -->
<!-- ## Custom UI

The color picker UI can be customized in all possible ways. The following sample shows the excel like UI customization with help of SplitButton and Dialog component. In that by clicking the more colors option from color palette, the dialog contains color picker will open.

{% tab template="colorpicker/position", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ColorPickerComponent, PaletteTileEventArgs, ColorPickerEventArgs } from '@syncfusion/ej2-react-inputs';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { SplitButtonComponent, BeforeOpenCloseMenuEventArgs, OpenCloseMenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';

class App extends React.Component<{}, {}> {
    public splitIcon: HTMLElement;
    public splitBtn: SplitButtonComponent;
    public colorPicker: ColorPickerComponent;
    public pickerDlg: DialogComponent;

    private animationSettings: Object = { effect: 'Zoom' };

    content(data: any): JSX.Element {
        let proxy: any = this;
        return (
            <div className="dialogContent">
                <ColorPickerComponent id='picker' inline={true} modeSwitcher={false} change={proxy.onPickerChange} ref={(scope) => { proxy.colorPicker = scope; }}></ColorPickerComponent>
            </div>
        )
    }

    public onPaletteChange (args: ColorPickerEventArgs): void {
        this.splitIcon.style.borderBottomColor = args.currentValue.rgba;
    }

    public onPickerChange(args: ColorPickerEventArgs): void {
        this.onPaletteChange(args);
        this.pickerDlg.hide();
    }

    public onDdPopupOpen(args: OpenCloseMenuEventArgs): void {
        args.element.children[1].addEventListener('click', this.openPickerDlg.bind(this));
    }

    public onBeforeDdPopupClose (args: BeforeOpenCloseMenuEventArgs): void {
        args.element.children[1].removeEventListener('click', this.openPickerDlg.bind(this));
    }

    public openPickerDlg(): void {
        this.pickerDlg.show();
    }

    public pickerDlgOpen(): void {
        this.colorPicker.refresh();
        this.colorPicker.element.nextElementSibling.querySelector('.e-ctrl-btn .e-cancel').addEventListener('click', this.pickerDlgClose.bind(this));
    }

    public pickerDlgClose(): void {
        this.pickerDlg.hide();
    }

    public onSplitBtnCreated() {
       this.splitIcon = this.element.children[0] as HTMLElement;
    }

    render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <ul id="target" tabindex="0">
                    <li className="e-item e-palette-item">
                        <ColorPickerComponent id='palette' mode='Palette' inline={true} showButtons={false} modeSwitcher={false} change={this.onPaletteChange.bind(this)}></ColorPickerComponent>
                    </li>
                    <li className="e-item" tabindex="-1">
                        <span className="e-menu-icon"></span>
                        More colors...
                    </li>
                </ul>
                <h4>Select color</h4>
                <SplitButtonComponent id='split-btn' created={this.onSplitBtnCreated} iconCss='e-icons e-font-icon' target='#target' open={this.onDdPopupOpen.bind(this)} beforeClose={this.onBeforeDdPopupClose.bind(this)}></SplitButtonComponent>
                <DialogComponent id='picker-dialog' cssClass='e-dlg-picker' isModal={true} height='336px' width='270px' ref={ dialog => this.pickerDlg = dialog} target='.wrap' content= {this.content.bind(this)} overlayClick={this.pickerDlgClose.bind(this)} open={this.pickerDlgOpen.bind(this)} visible={false} animationSettings={this.animationSettings}></DialogComponent>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %} -->

