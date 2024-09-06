---
title: "Template"
component: "Spreadsheet"
description: "This section helps you to learn how to add other controls in the Essential JS 2 Spreadsheet."
---

# Cell Template

Cell Template is used for adding HTML elements into Spreadsheet. You can add the cell template in spreadsheet by using the `template` property and specify the address using the `address` property inside the `ranges` property. You can customize the Html elements similar to Syncfusion components (TextBox, DropDownList, RadioButton, MultiSelect, DatePicker etc) by using the `beforeCellRender` event. In this demo, Cell template is applied to `C2:C9` and instantiated with Html input components like TextBox, RadioButton, TextArea. You need to bind the events to perform any operations through HTML elements or Syncfusion components. Here, we have added `change` event in to the MultiSelect control, and we have updated the selected data into the spreadsheet cell through that change event.

The following sample describes the above behavior.

Sample link: [`Cell template`](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/cell-template)

<!-- {% tab template="spreadsheet/template", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true %, compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective, RowsDirective, RowDirective, CellDirective, CellsDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective, getRangeIndexes, ChangeEventArgs, Row, RowModel} from '@syncfusion/ej2-react-spreadsheet';
import { TextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { RadioButtonComponent, ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { DropDownListComponent, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import { SelectionSettingsModel } from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
     constructor() {
        super(...arguments);
        this.scrollSettings = { isFinite: true };
        this.selectionSettings = { mode: 'None' };
        this.boldCenter = { fontWeight: 'bold', textAlign: 'center', fontSize: '12pt', verticalAlign: 'middle',
            textDecoration: 'underline'
        };
    }
    nameTextbox() {
        return (<TextBoxComponent placeholder="Name"></TextBoxComponent>);
    }
    dobTextbox() {
        return (<TextBoxComponent placeholder="DOB"></TextBoxComponent>);
    }
    genderRadioButton() {
        return (<div>
                <RadioButtonComponent name="gender" value="male" label="Male"></RadioButtonComponent>
                <RadioButtonComponent name="gender" value="female" label="Female"></RadioButtonComponent>
            </div>);
    }
    dropDownList() {
        let experience = ['0 - 1 year', '1 - 3 years', '3 - 5 years', '5 - 10 years'];
        return (<DropDownListComponent placeholder="Experience" dataSource={experience}></DropDownListComponent>);
    };
    multiSelect() {
        let languages = ['JAVA', 'C#', 'SQL'];
        return (<MultiSelectComponent placeholder="Areas of Interest" showClearButton={false} dataSource={languages}></MultiSelectComponent>);
    };
    mobileNoTextbox() {
        return (<TextBoxComponent placeholder="Mobile Number"></TextBoxComponent>);
    }
    emailTextbox() {
        return (<TextBoxComponent placeholder="Email"></TextBoxComponent>);
    }
    textArea() {
        return (<TextBoxComponent multiline={true}></TextBoxComponent>);
    }
    button() {
        return (<ButtonComponent content="Add" style={{ float: "right" }} cssClass="e-flat"></ButtonComponent>);
    }
    onCreated() {
        this.spreadsheet.cellFormat({ fontWeight: 'bold' }, 'B2:B9');
        // Merges B1 and C1 cells
        this.spreadsheet.merge('B1:C1');
    }
    render() {
        return (<div className='control-pane'>
                <div className='control-section spreadsheet-control'>
                    <SpreadsheetComponent showRibbon={false} showFormulaBar={false} allowOpen={false} allowSave={false} ref={(ssObj) => { this.spreadsheet = ssObj; }} created={this.onCreated.bind(this)} name={'Candidates List'} scrollSettings={this.scrollSettings} allowEditing={false} selectionSettings={this.selectionSettings}>
                        <SheetsDirective>
                            <SheetDirective name='Registration Form' rowCount={40} colCount={30} showGridLines={false}>
                                <RowsDirective>
                                    <RowDirective height={55}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Interview Registration Form' style={this.boldCenter}></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Name:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Date of Birth:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Gender:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Year of Experience:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Areas of Interest:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Mobile Number:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={45}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Email:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                    <RowDirective height={82}>
                                        <CellsDirective>
                                            <CellDirective index={1} value='Address:'></CellDirective>
                                        </CellsDirective>
                                    </RowDirective>
                                </RowsDirective>
                                <ColumnsDirective>
                                    <ColumnDirective index={1} width={190}></ColumnDirective>
                                    <ColumnDirective width={350}></ColumnDirective>
                                </ColumnsDirective>
                                <RangesDirective>
                                    <RangeDirective template={this.nameTextbox} address='C2'></RangeDirective>
                                    <RangeDirective template={this.dobTextbox} address='C3'></RangeDirective>
                                    <RangeDirective template={this.genderRadioButton} address='C4'></RangeDirective>
                                    <RangeDirective template={this.dropDownList} address='C5'></RangeDirective>
                                    <RangeDirective template={this.multiSelect} address='C6'></RangeDirective>
                                    <RangeDirective template={this.mobileNoTextbox} address='C7'></RangeDirective>
                                    <RangeDirective template={this.emailTextbox} address='C8'></RangeDirective>
                                    <RangeDirective template={this.textArea} address='C9'></RangeDirective>
                                    <RangeDirective template={this.button} address='C11'></RangeDirective>
                                </RangesDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>
                </div>
            </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %} -->

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Worksheet](./worksheet)
* [Rows and columns](./rows-and-columns)