---
title: "Sort a range by custom list"
component: "Spreadsheet"
description: "Learn how to sort a range of cells by custom list."
---

# Sort a range by custom list

You can also define the sorting of cell values based on your own customized personal list. In this article, custom list is achieved using `custom sort comparer`.

In the following demo, the `Trustworthiness` column is sorted based on the custom lists `Perfect`, `Sufficient`, and `Insufficient`.

{% tab template="spreadsheet/custom-sort", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx


import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective, SortDescriptor, CellModel } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';
import { tradeData } from './datasource';
import { DataManager, DataUtil } from '@syncfusion/ej2-data';

export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
    public mySortComparer(x: CellModel, y: CellModel): number {
        // custom sort comparer to sort based on the custom list.
           let customList: string[] = ['Perfect', 'Sufficient', 'Insufficient'];
            let comparer: Function = DataUtil.fnSort('Ascending');
            return comparer(x ? customList.indexOf(x.value) : x, y ? customList.indexOf(y.value) : y);
           };
    public onDataBound(): void {
         if (this.spreadsheet.activeSheetIndex === 0) {
            this.spreadsheet.sort({sortDescriptors: { field: 'F',  sortComparer: this.mySortComparer }, containsHeader: true}, 'A1:H20');
        }
    }

    public onSortComplete(args): void{
         this.spreadsheet.selectRange(args.range);
        // code here.
    }
     render() {
        return  (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }} dataBound={this.onDataBound.bind(this)} sortComplete={this.onSortComplete.bind(this)}>
                        <SheetsDirective>
                            <SheetDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={tradeData}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={90}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## See Also

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)