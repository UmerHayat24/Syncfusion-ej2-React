---
title: "Cell Range"
component: "Spreadsheet"
description: "Learn the various operations that you can perform in range of cells of the Essential JS 2 Spreadsheet."
---

# Cell Range

A group of cells in a sheet is known as cell range.

## Wrap text

Wrap text allows you to display large content as multiple lines in a single cell. By default, the wrap text support is enabled. Use the [`allowWrap`](../api/spreadsheet/#allowwrap) property to enable or disable the wrap text support in spreadsheet.

Wrap text can be applied or removed to a cell or range of cells in the following ways,

* Using the `wrap` property in `cell`, you can enable or disable wrap text to a cell at initial load.
* Select or deselect wrap button from ribbon toolbar to apply or remove the wrap text to the selected range.
* Using the [`wrap`](../api/spreadsheet/#wrap) method, you can apply or remove the wrap text once the component is loaded.

The following code example shows the wrap text functionality in spreadsheet.

{% tab template="spreadsheet/wrap", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective, RowsDirective, RowDirective, CellDirective, CellsDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-react-spreadsheet';
import { CellStyleModel, getRangeIndexes } from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';
import { addClass, removeClass } from '@syncfusion/ej2-base';

export default class App extends React.Component<{}, {}> {
       public spreadsheet: SpreadsheetComponent;
       public oncreated(args): void{
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:H1');
        this.spreadsheet.cellFormat({ verticalAlign: 'middle' }, 'A1:H5');
        this.spreadsheet.cellFormat({ textAlign: 'center' }, 'A2:B5');
        this.spreadsheet.cellFormat({ textAlign: 'center' }, 'D2:D5');
        // To wrap the cells from E2 to E5 range
        this.spreadsheet.wrap('E2:E5');
        // To unwrap the H3 cell
        this.spreadsheet.wrap('H3', false);
    }
     render() {
        return  ( <div> <SpreadsheetComponent
                        ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.oncreated.bind(this)} showFormulaBar={false} >
                        <SheetsDirective>
                            <SheetDirective name={"Movie List"}>
                             <RowsDirective>
                                 <RowDirective height={30}>
                                 </RowDirective>
                                 <RowDirective>
                                     <CellsDirective>
                                     <CellDirective index={7} wrap={true}></CellDirective>
                                     </CellsDirective>
                                     </RowDirective>
                                     <RowDirective>
                                     <CellsDirective>
                                     <CellDirective index={7} wrap={true}></CellDirective>
                                     </CellsDirective>
                                     </RowDirective>
                                     <RowDirective>
                                     <CellsDirective>
                                     <CellDirective index={7} wrap={true}></CellDirective>
                                     </CellsDirective>
                                     </RowDirective>
                                     <RowDirective>
                                     <CellsDirective>
                                     <CellDirective index={7} wrap={true}></CellDirective>
                                     </CellsDirective>
                                     </RowDirective>
                                     </RowsDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={100} index={1}></ColumnDirective>
                                    <ColumnDirective width={140}></ColumnDirective>
                                    <ColumnDirective width={90}></ColumnDirective>
                                    <ColumnDirective width={150}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                    <ColumnDirective width={90}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent> </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));

```

{% endtab %}

### Limitations of Wrap text

The following features have some limitations in wrap text:

* Sorting with wrap text applied data.
* Merge with wrap text

## Merge cells

Merge cells allows users to span two or more cells in the same row or column into a single cell. When cells with multiple values are merged, top-left most cell data will be the data for the merged cell. By default, the merge cells option is enabled. Use [`allowMerge`](../api/spreadsheet/#allowmerge) property to enable or disable the merge cells option in spreadsheet.

You can merge the range of cells in the following ways,

* Set the `rowSpan` and `colSpan` property in `cell` to merge the number of cells at initial load.
* Select the range of cells and apply merge by selecting the desired option from ribbon toolbar.
* Use [`merge`](../api/spreadsheet/#merge) method to merge the range of cells, once the component is loaded.

The available merge options in spreadsheet are,

| Type | Action |
|-------|---------|
| Merge All | Combines all the cells in a range in to a single cell (default). |
| Merge Horizontally | Combines cells in a range as row-wise. |
| Merge Vertically | Combines cells in a range as column-wise. |
| UnMerge | Splits the merged cells into multiple cells. |

The following code example shows the merge cells operation in spreadsheet.

{% tab template="spreadsheet/merge", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx


import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective, RowsDirective, RowDirective, CellsDirective, CellDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-react-spreadsheet';
import { CellStyleModel, getRangeIndexes } from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';
import { addClass, removeClass } from '@syncfusion/ej2-base';

export default class App extends React.Component<{}, {}> {
       public spreadsheet: SpreadsheetComponent;
    public boldRight: CellStyleModel = { fontWeight: 'bold', textAlign: 'right' };
    public bold: CellStyleModel = { fontWeight: 'bold' };
     public updateCollection(): void {
        let cell = this.spreadsheet.getActiveSheet().activeCell;
        let cellIdx = getRangeIndexes(cell);
        let Element= this.spreadsheet.getCell(cellIdx[0], cellIdx[1]);
        if (!Element.classList.contains("customClass")) {
            Element.classList.add('customClass'); // To add the custom class in active cell element
            this.spreadsheet.updateUndoRedoCollection({ eventArgs: { class: 'customClass', rowIdx: cellIdx[0], colIdx: cellIdx[1], action: 'customCSS' } }); // To update the undo redo collection
        }
    }

    public oncreated(): void{
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:S1');
        this.spreadsheet.numberFormat('h:mm AM/PM', 'C1:S1');
        this.spreadsheet.cellFormat({ verticalAlign: 'middle' }, 'A1:S11');
        // Merging the `K4:M4` cells using method
        this.spreadsheet.merge('K4:M4');
        // Merging the 5th and 6th row cells across 11th, 12th and 13th column
        this.spreadsheet.merge('K5:M6', 'Vertically');
        // Merging the 18th and 19th column cells across 2nd, 3rd and 4th row
        this.spreadsheet.merge('N4:O6', 'Horizontally');
    }
     render() {
        return  ( <div>
             <SpreadsheetComponent
                        ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.oncreated.bind(this)} showFormulaBar={false}>
                        <SheetsDirective>
                            <SheetDirective name={"Merge Cells"}>
                            <RowsDirective>
                                <RowDirective height={35}></RowDirective>
                                <RowDirective height={35}>
                                    <CellsDirective>
                                        <CellDirective index={1} rowSpan={2}></CellDirective>
                                        <CellDirective colSpan={2}></CellDirective>
                                        <CellDirective index={6} colSpan={3}></CellDirective>
                                        <CellDirective index={10} rowSpan={2} colSpan={3}></CellDirective>
                                        <CellDirective index={13} colSpan={2}></CellDirective>
                                        <CellDirective index={17} colSpan={2}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective height={35}>
                                    <CellsDirective>
                                        <CellDirective index={3} colSpan={3}></CellDirective>
                                        <CellDirective index={6} colSpan={4}></CellDirective>
                                        <CellDirective index={13} colSpan={3}></CellDirective>
                                        <CellDirective index={17} colSpan={2}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective height={35}>
                                    <CellsDirective>
                                        <CellDirective index={2} colSpan={3}></CellDirective>
                                        <CellDirective index={5} colSpan={2}></CellDirective>
                                        <CellDirective index={7} colSpan={3}></CellDirective>
                                        <CellDirective index={15} colSpan={2}></CellDirective>
                                        <CellDirective index={17} colSpan={2}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective height={35}>
                                    <CellsDirective>
                                        <CellDirective index={2} colSpan={3}></CellDirective>
                                        <CellDirective index={6} colSpan={4}></CellDirective>
                                        <CellDirective index={16} colSpan={2}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective height={35}>
                                    <CellsDirective>
                                        <CellDirective index={2} colSpan={4}></CellDirective>
                                        <CellDirective index={7} colSpan={3}></CellDirective>
                                        <CellDirective index={15} colSpan={2}></CellDirective>
                                        <CellDirective index={17} colSpan={2}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                            </RowsDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={90}></ColumnDirective>
                                    <ColumnDirective width={150}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent> </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));

```

{% endtab %}

### Limitations of Merge

The following features have some limitations in Merge:

* Merge with filter.
* Merge with wrap text.

## Data Validation

Data Validation is used to restrict the user from entering the invalid data. You can use the [`allowDataValidation`](../api/spreadsheet/#allowDataValidation) property to enable or disable data validation.

> * The default value for `allowDataValidation` property is `true`.

### Apply Validation

You can apply data validation to restrict the type of data or the values that users enter into a cell.

You can apply data validation by using one of the following ways,

* Select the Data tab in the Ribbon toolbar, and then choose the Data Validation item.
* Use the [`addDataValidation()`](../api/spreadsheet/#addDataValidation) method programmatically.

### Clear Validation

Clear validation feature is used to remove data validations from the specified ranges or the whole worksheet.

You can clear data validation rule by one of the following ways,

* Select the Data tab in the Ribbon toolbar, and then choose the Clear Validation item.
* Use the [`removeDataValidation()`](../api/spreadsheet/#removeDataValidation) method programmatically.

### Highlight Invalid Data

Highlight invalid data feature is used to highlight the previously entered invalid values.

You can highlight an invalid data by using one of the following ways,

* Select the Data tab in the Ribbon toolbar, and then choose the Highlight Invalid Data item.
* Use the [`addInvalidHighlight()`](../api/spreadsheet/#addInvalidHighlight) method programmatically.

### Clear Highlighted Invalid Data

Clear highlight feature is used to remove the highlight from invalid cells.

You can clear the highlighted invalid data by using the following ways,

* Select the Data tab in the Ribbon toolbar, and then choose the Clear Highlight item.
* Use the [`removeInvalidHighlight()`](../api/spreadsheet/#removeInvalidHighlight) method programmatically.

{% tab template="spreadsheet/data-validation", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective, RowsDirective, RowDirective, CellsDirective, CellDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-react-spreadsheet';
import { CellStyleModel, getRangeIndexes } from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';
import { addClass, removeClass } from '@syncfusion/ej2-base';

export default class App extends React.Component<{}, {}> {
    public spreadsheet: SpreadsheetComponent;
    public boldCenter: CellStyleModel = { fontWeight: 'bold', textAlign: 'center' };

    public oncreated(): void {
        //Add Data validation to range.
            this.spreadsheet.addDataValidation({ type: 'TextLength' , operator: 'LessThanOrEqualTo' , value1: '4' }, 'A2:A5');
            this.spreadsheet.addDataValidation({ type: 'WholeNumber', operator: 'NotEqualTo', value1: '1' }, 'B2:B5');
            this.spreadsheet.addDataValidation({ type: 'Date', operator: 'NotEqualTo', value1: '04/11/2019'}, 'F2:F5');
            this.spreadsheet.addDataValidation({ type: 'Time', operator: 'Between', value1: '10:00:00 AM', value2: '11:00:00 AM' }, 'G2:G5');
            this.spreadsheet.addDataValidation({ type: 'Decimal', operator: 'LessThan', value1: '100000.00'}, 'H2:H5');
            //Highlight Invalid Data.
            this.spreadsheet.addInvalidHighlight('A1:H5');
    }
     render() {
        return  ( <div>
             <SpreadsheetComponent
                        ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.oncreated.bind(this)} showFormulaBar={false}>
                        <SheetsDirective>
                            <SheetDirective name={'PriceDetails'}>
                            <RowsDirective>
                                <RowDirective index={0}>
                                    <CellsDirective>
                                        <CellDirective index={0} value={'Seller Name'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={1} value={'Customer Id'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={2} value={'Customer Name'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={3} value={'Product Name'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={4} value={'Product Price'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={5} value={'Sales Date'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={6} value={'Billing Time'} style={this.boldCenter}></CellDirective>
                                        <CellDirective index={7} value={'Total Price'} style={this.boldCenter}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective index={1}>
                                    <CellsDirective>
                                        <CellDirective index={0} value={'John'}></CellDirective>
                                        <CellDirective index={1} value={'1'} validation= {{ type: 'WholeNumber', operator: 'NotEqualTo', value1: '1'}}></CellDirective>
                                        <CellDirective index={2} value={'Nash'}></CellDirective>
                                        <CellDirective index={3} value={'Digger'} validation= {{ type: 'List', value1: 'Digger, Digger, Cherrypicker' }}></CellDirective>
                                        <CellDirective index={4} value={'50000'} validation= {{ type: 'List', value1: '50000,50000,45000' }}></CellDirective>
                                        <CellDirective index={5} value={'04/11/2019'}></CellDirective>
                                        <CellDirective index={6} value={'11:34:32 AM'}></CellDirective>
                                        <CellDirective index={7} value={'1,45,000.00'}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective index={2}>
                                    <CellsDirective>
                                        <CellDirective index={0} value={'Mike'}></CellDirective>
                                        <CellDirective index={1} value={'2'} validation= {{ type: 'WholeNumber', operator: 'NotEqualTo', value1: '1'}}></CellDirective>
                                        <CellDirective index={2} value={'Jim'}></CellDirective>
                                        <CellDirective index={3} value={'Cherrypicker'} validation= {{ type: 'List', value1: 'Cherrypicker, JCB, Wheelbarrow' }}></CellDirective>
                                        <CellDirective index={4} value={'45000'} validation= {{ type: 'List', value1: '45000,90000,40' }}></CellDirective>
                                        <CellDirective index={5} value={'04/11/2019'}></CellDirective>
                                        <CellDirective index={6} value={'11:34:32 AM'}></CellDirective>
                                        <CellDirective index={7} value={'1,45,000.00'}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective index={3}>
                                    <CellsDirective>
                                        <CellDirective index={0} value={'shane'}></CellDirective>
                                        <CellDirective index={1} value={'3'} validation= {{ type: 'WholeNumber', operator: 'NotEqualTo', value1: '1'}}></CellDirective>
                                        <CellDirective index={2} value={'Sean'}></CellDirective>
                                        <CellDirective index={3} value={'Kango'} validation= {{ type: 'List', value1: 'Kango, Ropes' }}></CellDirective>
                                        <CellDirective index={4} value={'450'} validation= {{ type: 'List', value1: '450, 95' }}></CellDirective>
                                        <CellDirective index={5} value={'06/25/2019'}></CellDirective>
                                        <CellDirective index={6} value={'01:30:11 PM'}></CellDirective>
                                        <CellDirective index={7} value={'545.00'}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                                <RowDirective index={4}>
                                    <CellsDirective>
                                        <CellDirective index={0} value={'John'}></CellDirective>
                                        <CellDirective index={1} value={'1'} validation= {{ type: 'WholeNumber', operator: 'NotEqualTo', value1: '1'}}></CellDirective>
                                        <CellDirective index={2} value={'Nash'}></CellDirective>
                                        <CellDirective index={3} value={'JCB'} validation= {{ type: 'List', value1: 'JCB, Ropes, scaffolding' }}></CellDirective>
                                        <CellDirective index={4} value={'90000'} validation= {{ type: 'List', value1: '90000, 95, 10000' }}></CellDirective>
                                        <CellDirective index={5} value={'09/22/2019'}></CellDirective>
                                        <CellDirective index={6} value={'12:30:02 PM'}></CellDirective>
                                        <CellDirective index={7} value={'1,00,095.00'}></CellDirective>
                                    </CellsDirective>
                                </RowDirective>
                            </RowsDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={88}></ColumnDirective>
                                    <ColumnDirective width={88}></ColumnDirective>
                                    <ColumnDirective width={106}></ColumnDirective>
                                    <ColumnDirective width={98}></ColumnDirective>
                                    <ColumnDirective width={88}></ColumnDirective>
                                    <ColumnDirective width={86}></ColumnDirective>
                                    <ColumnDirective width={107}></ColumnDirective>
                                    <ColumnDirective width={81}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent> </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));

```

{% endtab %}

### Limitations of Data validation

The following features have some limitations in Data Validation:

* Entire row data validation.
* Insert row between the data validation.
* Copy/paste with data validation.
* Delete cells between data validation applied range.

## Clear

Clear feature helps you to clear the cell contents (formulas and data), formats (including number formats, conditional formats, and borders) in a spreadsheet. When you apply clear all, both the contents and the formats will be cleared simultaneously.

### Apply Clear Feature

You can apply clear feature by using one of the following ways,

* Select the clear icon in the Ribbon toolbar under the Home Tab.
* Using the [`clear()`](../api/spreadsheet/#clear) method to clear the values.

Clear has the following types in the spreadsheet,

| Options | Uses |
|-----|------|
| `Clear All` | Used to clear all contents, formats, and hyperlinks.  |
| `Clear Formats` | Used to clear the formats (including number formats, conditional formats, and borders) in a cell. |
| `Clear Contents` | Used to clear the contents (formulas and data) in a cell. |
| `Clear Hyperlinks` | Used to clear the hyperlink in a cell. |

### Methods

Clear the cell contents and formats in the Spreadsheet document by using the [clear](../api/spreadsheet/#clear) method. The [clear](../api/spreadsheet/#clear) method has `type` and `range` as parameters. The following code example shows how to clear the cell contents and formats in the button click event.

{% tab template="spreadsheet/clear", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px",  compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
import { getComponent } from '@syncfusion/ej2-base';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';
export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
    public items: ItemModel[] = [
    {
        text: "Clear All"
    },
    {
        text: "Clear Formats"
    },
    {
        text: "Clear Contents"
    },
    {
        text: "Clear Hyperlinks"
    }
    ];
    public oncreated(args): void{
        this.spreadsheet.cellFormat({ fontWeight: 'bold', fontSize: '12pt'}, 'A1:E1');
        this.spreadsheet.cellFormat({ color: '#10c469' }, 'B1:B10');
    }
    public itemSelect(args): void {
        let spreadsheet = getComponent(document.getElementById("spreadsheet"), "spreadsheet");
        if (args.item.text === 'Clear All')
            spreadsheet.clear({ type: 'Clear All', range: 'D1:D10' }); // Clear the content, formats and hyperlinks applied in the provided range.
        if (args.item.text === 'Clear Formats')
            spreadsheet.clear({ type: 'Clear Formats', range: 'B1:B10' }); // Clear the formats applied in the provided range
        if (args.item.text === 'Clear Contents')
            spreadsheet.clear({ type: 'Clear Contents', range: 'A1:A10' }); // Clear the content in the provided range
        if (args.item.text === 'Clear Hyperlinks')
            spreadsheet.clear({ type: 'Clear Hyperlinks', range: 'F2:F6' }); // Clear the hyperlinks applied in the provided range
    }
     render() {
        return  ( <div><DropDownButtonComponent id="element" items={this.items} select={this.itemSelect}> Clear </DropDownButtonComponent>
        <SpreadsheetComponent id ='spreadsheet' ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.oncreated.bind(this)}>
                        <SheetsDirective>
                            <SheetDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={110}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent> </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Rows and columns](./rows-and-columns)
* [Formatting](./formatting)
* [Hyperlink](./link)
* [Sorting](./sort)
* [Filtering](./filter)
