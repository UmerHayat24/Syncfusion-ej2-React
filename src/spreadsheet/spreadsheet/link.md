---
title: "Hyperlink"
component: "Spreadsheet"
description: "This section helps to learn how to insert, edit and remove a hyperlink in Spreadsheet control."
---

# Hyperlink

Hyperlink is used to navigate to web links or cell reference within the sheet or to other sheets in Spreadsheet. You can use the [`allowHyperlink`](../api/spreadsheet/#allowHyperlink) property to enable or disable hyperlink functionality.

> * The default value for `allowHyperlink` property is `true`.

## Insert Link

You can insert a hyperlink in a worksheet cell for quick access to related information.

**User Interface**:

In the active spreadsheet, click the cell where you want to create a hyperlink. Insert hyperlink can be done by any of the following ways:
* Select the INSERT tab in the Ribbon toolbar and choose the `Link` item.
* Right-click the cell and then click Hyperlink item in the context menu, or you can press Ctrl+K.
* Use the [`addHyperlink()`](../api/spreadsheet/#hyperlink) method programmatically.

## Edit Hyperlink

You can change an existing hyperlink in your workbook by changing its destination or the text that is used to represent it.

**User Interface**:

In the active spreadsheet, Select the cell that contains the hyperlink that you want to change. Editing the hyperlink while opening the dialog can be done by any one of the following ways:

* Select the INSERT tab in the Ribbon toolbar and choose the `Link` item.
* Right-click the cell and then click Edit Hyperlink item in the context menu, or you can press Ctrl+K.

In the Edit Link dialog box, make the changes that you want, and click UPDATE.

## Remove Hyperlink

Performing this operation remove a single hyperlink without losing the display text.

**User Interface**:

In the active spreadsheet, click the cell where you want to remove a hyperlink. remove hyperlink can be done by any of the following ways:
* Right-click the cell and then click Remove Hyperlink item in the context menu.
* Use the [`removeHyperlink()`](../api/spreadsheet/#hyperlink) method programmatically.

## How to change target attribute

There is an event named `beforeHyperlinkClick` which triggers only on clicking hyperlink. You can customize where to open the hyperlink by using the `target` property in the arguments of that event.

{% tab template="spreadsheet/link", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, CellDirective, RowDirective } from '@syncfusion/ej2-react-spreadsheet';
import { ColumnsDirective, ColumnDirective, CellsDirective, RowsDirective } from '@syncfusion/ej2-react-spreadsheet';
export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
public onbeforeHyperlinkClick(args): void {
     args.target = '_self'; //change target attribute
}
    render() {
        return (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }} beforeHyperlinkClick={this.onbeforeHyperlinkClick.bind(this)}>
            <SheetsDirective>
                <SheetDirective selectedRange='D13' name='PriceDetails'>
                    <RowsDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Item Name' ></CellDirective>
                                <CellDirective value='Quantity' ></CellDirective>
                                <CellDirective value='Price' ></CellDirective>
                                <CellDirective value='Amount' ></CellDirective>
                                <CellDirective value='Stock Detail' ></CellDirective>
                                <CellDirective value='Website' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Casual Shoes' ></CellDirective>
                                <CellDirective value='10' ></CellDirective>
                                <CellDirective value='20' ></CellDirective>
                                <CellDirective value='200' ></CellDirective>
                                <CellDirective value='OUT OF STOCK' ></CellDirective>
                                <CellDirective value='Amazon' hyperlink='https://www.amazon.com/'></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Sports Shoes' ></CellDirective>
                                <CellDirective value='20' ></CellDirective>
                                <CellDirective value='30' ></CellDirective>
                                <CellDirective value='600'></CellDirective>
                                <CellDirective value='IN STOCK' hyperlink='Stock!A2:B2' ></CellDirective>
                                <CellDirective value='Overstack' hyperlink='https://www.overstock.com/'></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Formal Shoes' ></CellDirective>
                                <CellDirective value='20' ></CellDirective>
                                <CellDirective value='15' ></CellDirective>
                                <CellDirective value='300'></CellDirective>
                                <CellDirective value='IN STOCK' hyperlink='Stock!A3:B3' ></CellDirective>
                                <CellDirective value='AliExpress' hyperlink='https://www.aliexpress.com/'></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Sandals & Floaters' ></CellDirective>
                                <CellDirective value='15' ></CellDirective>
                                <CellDirective value='20' ></CellDirective>
                                <CellDirective value='300' ></CellDirective>
                                <CellDirective value='OUT OF STOCK' ></CellDirective>
                                <CellDirective value='AliBaba' hyperlink='https://www.alibaba.com/'></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Flip-Flops & Slippers' ></CellDirective>
                                <CellDirective value='30' ></CellDirective>
                                <CellDirective value='10' ></CellDirective>
                                <CellDirective value='300'></CellDirective>
                                <CellDirective value='IN STOCK' hyperlink='Stock!A4:B4' ></CellDirective>
                                <CellDirective value='Taobao' hyperlink='https://taobao.com/'></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                    </RowsDirective>
                    <ColumnsDirective>
                        <ColumnDirective width={110}></ColumnDirective>
                        <ColumnDirective width={115}></ColumnDirective>
                        <ColumnDirective width={110}></ColumnDirective>
                        <ColumnDirective width={100}></ColumnDirective>
                        <ColumnDirective width={110}></ColumnDirective>
                        <ColumnDirective width={100}></ColumnDirective>
                    </ColumnsDirective>
                </SheetDirective>
                <SheetDirective selectedRange='D13' name='Stock'>
                    <RowsDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Item Name' ></CellDirective>
                                <CellDirective value='Available Count' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Casual Shoes' ></CellDirective>
                                <CellDirective value='10' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Sports Shoes' ></CellDirective>
                                <CellDirective value='20' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Formal Shoes' ></CellDirective>
                                <CellDirective value='20' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Sandals & Floaters' ></CellDirective>
                                <CellDirective value='15' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                        <RowDirective>
                            <CellsDirective>
                                <CellDirective value='Flip-Flops & Slippers' ></CellDirective>
                                <CellDirective value='30' ></CellDirective>
                            </CellsDirective>
                        </RowDirective>
                    </RowsDirective>
                    <ColumnsDirective>
                        <ColumnDirective width={110}></ColumnDirective>
                        <ColumnDirective width={115}></ColumnDirective>
                    </ColumnsDirective>
                </SheetDirective>
            </SheetsDirective>
        </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));

```

{% endtab %}

## Limitations

* Inserting hyperlink not supported for multiple ranges.

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Sorting](./sort)
* [Filtering](./filter)
* [Undo Redo](./undo-redo)