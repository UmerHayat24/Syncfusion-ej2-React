---
title: "Ribbon"
component: "Spreadsheet"
description: "Learn the various operations that you can perform in ribbon of the Essential JS 2 Spreadsheet."
---

# Ribbon

It helps to organize a spreadsheet’s features into a series of tabs. By clicking the expand or collapse icon, you can expand or collapse the ribbon toolbar dynamically.

## Ribbon Customization

You can customize the ribbon using the following methods,

| Method | Action |
|-------|---------|
| [`hideRibbonTabs`](../api/spreadsheet/#hideribbontabs) | Used to show or hide the existing ribbon tabs. |
| [`enableRibbonTabs`](../api/spreadsheet/#enableribbontabs) | Used to enable or disable the existing
ribbon tabs. |
| [`addRibbonTabs`](../api/spreadsheet/#addribbontabs) | Used to add custom ribbon tabs. |
| [`hideToolbarItems`](../api/spreadsheet/#hidetoolbaritems) | Used to show or hide the existing ribbon
toolbar items. |
| [`enableToolbarItems`](../api/spreadsheet/#enabletoolbaritems) | Used to enable or disable the specified
toolbar items. |
| [`addToolbarItems`](../api/spreadsheet/#addtoolbaritems) | Used to add the custom items in ribbon
toolbar. |
| [`hideFileMenuItems`](../api/spreadsheet/#hidefilemenuitems) | Used to show or hide the ribbon file menu
items. |
| [`enableFileMenuItems`](../api/spreadsheet/#enablefilemenuitems) | Used to enable or disable file menu items. |
| [`addFileMenuItems`](../api/spreadsheet/#addfilemenuitems) | Used to add custom file menu items. |

The following code example shows the usage of ribbon customization.

{% tab template="spreadsheet/ribbon", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { select } from '@syncfusion/ej2-base';
import { RangeDirective, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
       public spreadsheet: SpreadsheetComponent;
       public created(): void{
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:F1');
        // Hiding the `Insert` from ribbon.
        this.spreadsheet.hideRibbonTabs(['Insert']);
        // Set disabled state to `View` ribbon tab.
        this.spreadsheet.enableRibbonTabs(['View'], false);
        // Adding the `Help` ribbon tab at the last index.
        // Specify the ribbon tab header text in last optional argument(`insertBefore`) for inserting new tab before any existing tab.
        this.spreadsheet.addRibbonTabs([{ header: { text: 'Help' }, content: [{ text: 'Feedback', tooltipText: 'Feedback',
            click: (): void => { /* Any click action for this toolbar item will come here. */ } }] }]);
        // Hiding the unwanted toolbar items from `Home` by specifying its index.
        this.spreadsheet.hideToolbarItems('Home', [0, 1, 2, 4, 14, 15, 21, 24]);
        // Set disable state to `Underline`, 'Wrap text` toolbar items from `Home` by specifying the item id.
        this.spreadsheet.enableToolbarItems('Home', [`${this.spreadsheet.element.id}_underline`, `${this.spreadsheet.element.id}_wrap`], false);
        // Set disable state to `Protect Sheet` toolbar item from `Data` by mentioning its index.
        this.spreadsheet.enableToolbarItems('Data', [0], false);
        // Adding the new `Custom Formulas` toolbar item under `Formulas` tab for adding custom formulas.
        this.spreadsheet.addToolbarItems(
            'Formulas', [{ type: 'Separator' }, {
                text: 'Custom Formulas', tooltipText: 'Custom Formulas',
                // You can set click handler for each new custom toolbar item
                click: (): void => {
                    // You can add custom formulas here.
                }
            }]);
        // Adding new custom item `Import` after the existing `Open` item. By default, new item will add after the specified item.
        this.spreadsheet.addFileMenuItems([{ text: 'Import', iconCss: 'e-open e-icons' }], 'Open');
        // Adding new custom item `Export As` after the existing `Save As` item.
        // Set `insertAfter` optional argument as `false` for adding new item before the specified item.
        this.spreadsheet.addFileMenuItems(
            [{
                text: 'Export As', iconCss: 'e-save e-icons', items: [{ text: 'XLSX', iconCss: 'e-xlsx e-icons' },
                    { text: 'XLS', iconCss: 'e-xls e-icons' }, { text: 'CSV', iconCss: 'e-csv e-icons' }]
            }],
            'Save As', false);
    };
    public fileMenuBeforeOpen(): void{
        // Because the file menu items are created dynamically, you need to perform the hide or show and enable/disable operations
        // under filemenu before open event.
        // Hiding the `Save As` and `Open` item.
        this.spreadsheet.hideFileMenuItems(['Save As', 'Open']);
         // Set disable state to `New` item. You can perform any file menu items customization by specifying the item id,
        // if it has more than one same item text. Set the last argument `isUniqueId` as true for using the item id.
        this.spreadsheet.enableFileMenuItems([`${this.spreadsheet.element.id}_New`], false, true);
    }
    public fileMenuItemSelect(args): void{
         // Custom file menu items select handler
         switch (args.item.text) {
            case 'Import': select(`#${this.spreadsheet.element.id}_fileUpload`, this.spreadsheet.element).click();
                break;
            case 'XLSX': this.spreadsheet.save({ saveType: 'Xlsx' });
                break;
            case 'XLS': this.spreadsheet.save({ saveType: 'Xls' });
                break;
            case 'CSV': this.spreadsheet.save({ saveType: 'Csv' });
                break;
        }
    }
     render() {
        return  ( <div>
        <SpreadsheetComponent
                        ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.created.bind(this)} fileMenuBeforeOpen={this.fileMenuBeforeOpen.bind(this)} fileMenuItemSelect={this.fileMenuItemSelect.bind(this)}
                        showFormulaBar={false} showSheetTabs={false} allowInsert={false} allowDelete={false} allowMerge={false} openUrl="https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/open"
                        saveUrl="https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save">
                        <SheetsDirective>
                            <SheetDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={120}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>
                   </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));


```

{% endtab %}

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Worksheet](./worksheet)
* [Rows and columns](./rows-and-columns)
