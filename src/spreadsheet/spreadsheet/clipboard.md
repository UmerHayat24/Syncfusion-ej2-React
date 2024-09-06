---
title: "Clipboard"
component: "Spreadsheet"
description: "This section explains you about the Clipboard feature (cut, copy, paste) in the Essential JS 2 spreadsheet."
---

# Clipboard

The Spreadsheet provides support for the clipboard operations (cut, copy, and paste). Clipboard operations can be enabled or disabled by setting the [`enableClipboard`](../api/spreadsheet/#enableclipboard) property in Spreadsheet.

> By default, the `enableClipboard` property is true.

## Cut

It is used to cut the data from selected range of cells, rows or columns in a spreadsheet and make it available in the clipboard.

**User Interface**:

Cut can be done in one of the following ways.

* Using Cut button in the Ribbon’s HOME tab to perform cut operation.
* Using Cut option in the Context Menu.
* Using `Ctrl + X` | `Command + X` keyboard shortcut.
* Using the [`cut`](../api/spreadsheet/#cut) method.

## Copy

It is used to copy the data from selected range of cells, rows or columns in a spreadsheet and make it available in the clipboard.

**User Interface**:

Copy can be done in one of the following ways.

* Using Copy button in the Ribbon’s HOME tab to perform copy operation.
* Using Copy option in the Context Menu.
* Using `Ctrl + C` | `Command + C` keyboard shortcut.
* Using the [`copy`](../api/spreadsheet/#copy) method.

## Paste

It is used to paste the clipboard data to the selected range, rows or columns. You have the following options in Paste,

* `Paste Special` - You can paste the values with formatting.
* `Paste` - You can paste only the values without formatting.

It also performs for external clipboard operation. If you perform cut and paste, clipboard data will be cleared, whereas in copy and paste the clipboard contents will be maintained. If you perform paste inside the copied range, the clipboard data will be cleared.

**User Interface**:

Paste can be done in one of the following ways.

* Using Paste button in the Ribbon’s HOME tab to perform paste operation.
* Using Paste option in the Context Menu.
* Using `Ctrl + V` | `Command + V` keyboard shortcut.
* Using the [`paste`](../api/spreadsheet/#paste) method.

> If you use the Keyboard shortcut key for cut (`Ctrl + X`) | copy (`Ctrl + C`) from other sources, you should use `Ctrl + V` shortcut while pasting into the spreadsheet.

{% tab template="spreadsheet/clipboard", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import {getComponent} from '@syncfusion/ej2-base';
import { RangeDirective, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-react-spreadsheet';
import { defaultData } from './datasource';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';

export default class App extends React.Component<{}, {}> {
    public spreadsheet: SpreadsheetComponent;
    public items: ItemModel[] = [
    {
        text: "Cut"
    },
    {
        text: "Copy"
    },
    {
        text: "Paste"
    }];
    public oncreated(): void{
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center', verticalAlign: 'middle' }, 'A1:H1');
    }
    public itemSelect(args): void {
        let spreadsheet = getComponent(document.getElementById("spreadsheet"), "spreadsheet");
        if (args.item.text === 'Cut')
            spreadsheet.cut();
        if (args.item.text === 'Copy')
            spreadsheet.copy();
        if (args.item.text === 'Paste')
            spreadsheet.paste();
    }
     render() {
        return  ( <div>
        <DropDownButtonComponent id="element" items={this.items} select={this.itemSelect}> Clipboard </DropDownButtonComponent>
             <SpreadsheetComponent id="spreadsheet"     ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.oncreated.bind(this)} enableClipboard={true}>
                        <SheetsDirective>
                            <SheetDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={defaultData}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={92}></ColumnDirective>
                                    <ColumnDirective width={96}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent> </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Prevent the paste functionality

The following example shows, how to prevent the paste action in spreadsheet. In [`actionBegin`](../api/spreadsheet/#actionbegin) event, you can set `cancel` argument as false in paste request type.

{% tab template="spreadsheet/clipboard", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import {getComponent} from '@syncfusion/ej2-base';
import { RangeDirective, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-react-spreadsheet';
import { defaultData } from './datasource';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';

export default class App extends React.Component<{}, {}> {
    public spreadsheet: SpreadsheetComponent;
    public items: ItemModel[] = [
    {
        text: "Cut"
    },
    {
        text: "Copy"
    },
    {
        text: "Paste"
    }];
    public onCreated(): void{
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center', verticalAlign: 'middle' }, 'A1:H1');
    }
    public onActionBegin(pasteArgs): void{
        if (pasteArgs.args.eventArgs.requestType === 'paste') {
            pasteArgs.args.eventArgs.cancel = true;
        }
    }
    public itemSelect(args): void {
        let spreadsheet = getComponent(document.getElementById("spreadsheet"), "spreadsheet");
        if (args.item.text === 'Cut')
            spreadsheet.cut();
        if (args.item.text === 'Copy')
            spreadsheet.copy();
        if (args.item.text === 'Paste')
            spreadsheet.paste();
    }
     render() {
        return  ( <div><DropDownButtonComponent id="element" items={this.items} select={this.itemSelect}> Clipboard </DropDownButtonComponent>
             <SpreadsheetComponent id="spreadsheet"
                        ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.onCreated.bind(this)} actionBegin={this.onActionBegin.bind(this)} enableClipboard={true}>
                        <SheetsDirective>
                            <SheetDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={defaultData}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={92}></ColumnDirective>
                                    <ColumnDirective width={96}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent> </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Limitations

* External clipboard is not fully supported while copying data from another source and pasting into a spreadsheet, it only works with basic supports (Values, Number, cell, and Text formatting).
* If you copy =SUM(A2,B2) and paste, the formula reference will change depending on the pasted cell address but we don't have support for nested formula(formula reference will be same).
* Clipboard is not supported with conditional formatting (values only pasting).
* We have limitation while copying the whole sheet data and pasting it into another sheet.

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.