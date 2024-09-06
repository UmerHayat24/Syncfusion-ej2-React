---
title: "Globalization"
component: "TreeGrid"
description: "Learn how to apply localization (l10n), internationalization (i18n), and right-to-left (RTL) in Essential JS 2 TreeGrid control."
---

# Globalization

## Localization

The [`Localization`](../common/localization) library allows you to localize default text content of the TreeGrid. The treegrid component has static text on some features (like toolbar area text, filter menu text, pager information text, etc.) that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/treegrid/#locale) value and translation object.

The following list of properties and its values are used in the treegrid.

Locale keywords |Text
-----|-----
EmptyRecord | No records to display
True | true
False | false
ExpandAll | Expand All
CollapseAll | Collapse All
InvalidFilterMessage | Invalid Filter Data
FilterbarTitle | \s filter bar cell
Add | Add
Edit| Edit
Cancel| Cancel
Update| Update
Delete | Delete
Print | Print
Pdfexport | PDF Export
Excelexport | Excel Export
Wordexport | Word Export
Csvexport | CSV Export
Search | Search
Save | Save
EditOperationAlert | No records selected for edit operation
DeleteOperationAlert | No records selected for delete operation
SaveButton | Save
OKButton | OK
CancelButton | Cancel
EditFormTitle | Details of
AddFormTitle | Add New Record
ConfirmDelete | Are you sure you want to Delete Record?
SearchColumns | search columns
Matchs | No Matches Found
FilterButton | Filter
ClearButton | Clear
StartsWith | Starts With
EndsWith | Ends With
Contains | Contains
Equal | Equal
NotEqual | Not Equal
LessThan | Less Than
LessThanOrEqual | Less Than Or Equal
GreaterThan | Greater Than
GreaterThanOrEqual | Greater Than Or Equal
ChooseDate | Choose a Date
EnterValue | Enter the value
autoFitAll | Auto Fit all columns
autoFit | Auto Fit this column
Export | Export
FirstPage | First Page
LastPage | Last Page
PreviousPage | Previous Page
NextPage | Next Page
SortAscending | Sort Ascending
SortDescending | Sort Descending
EditRecord | Edit Record
DeleteRecord | Delete Record
Above | Above
Below | Below
AddRow | Add Row
FilterMenu | Filter
SelectAll | Select All
Blanks | Blanks
FilterTrue | True
FilterFalse | False
NoResult | No Matches Found
ClearFilter | Clear Filter
NumberFilter | Number Filters
TextFilter | Text Filters
DateFilter | Date Filters
MatchCase | Match Case
Between | Between
CustomFilter | Custom Filter
CustomFilterPlaceHolder | Enter the value
CustomFilterDatePlaceHolder | Choose a date
AND | AND
OR | OR
ShowRowsWhere | Show rows where:
currentPageInfo | {0} of {1} pages
totalItemsInfo | ({0} items)
firstPageTooltip | Go to first page
lastPageTooltip | Go to last page
nextPageTooltip | Go to next page
previousPageTooltip | Go to previous page
nextPagerTooltip | Go to next pager
previousPagerTooltip | Go to previous pager
pagerDropDown | Items per page
pagerAllDropDown | Items
All | All

### Loading translations

To load translation object in an application, use [`load`](https://ej2.syncfusion.com/documentation/api/base/l10n/#load) function of the [`L10n`](https://ej2.syncfusion.com/documentation/api/base/l10n/) class.

The following example demonstrates the TreeGrid in *Deutsch* culture.

{% tab template="treegrid/internationalization", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, FilterSettingsModel, Inject, PageSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

L10n.load({
    'de-DE': {
        'pager': {
            'currentPageInfo': '{0} von {1} Seiten',
            'firstPageTooltip': 'Zur ersten Seite',
            'lastPageTooltip': 'Zur letzten Seite',
            'nextPageTooltip': 'Zur nächsten Seite',
            'nextPagerTooltip': 'Zum nächsten Pager',
            'previousPageTooltip': 'Zurück zur letzten Seit',
            'previousPagerTooltip': 'Zum vorherigen Pager',
            'totalItemsInfo': '({0} Beiträge)'
        },
        'treegrid': {
            "ClearButton": "klar",
            'Collapse All': 'Alles einklappen',
            "Contains": "Enthält",
            'EmptyRecord': 'Keine Aufzeichnungen angezeigt',
            "EndsWith": "Endet mit",
            "EnterValue": "Geben Sie den Wert ein",
            "Equal": "Gleich",
            "Excelexport": "Excel-Export",
            'Expand All': 'Alle erweitern',
            "FilterButton": "Filter",
            "FilterMenu": "Filter",
            "GreaterThan": "Größer als",
            "GreaterThanOrEqual": "Größer als oder gleich",
            "LessThan": "Weniger als",
            "LessThanOrEqual": "Weniger als oder gleich",
            "NotEqual": "Nicht gleich",
            "Pdfexport": "PDF-Export",
            "Print": "Drucken",
            "StartsWith": "Beginnt mit",
            "Wordexport": "Word-Export"
        }
    }
});

export default class App extends React.Component<{}, {}>{

    public FilterOptions: FilterSettingsModel = {
        type: 'Menu'
    };
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public toolbarOptions: ToolbarItems[] = ['Print'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
         allowPaging='true' pageSettings={this.pageSettings} locale='de-DE' allowFiltering='true'
        filterSettings={this.FilterOptions} toolbar={this.toolbarOptions} height='220'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Internationalization

The [`Internationalization`](../common/internationalization/) library is used to globalize number, date, and time values in treegrid component using format strings in the [`columns.format`](../api/treegrid/column/#format).

{% tab template="treegrid/internationalization", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { L10n, loadCldr, setCulture, setCurrencyCode } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, FilterSettingsModel, Inject, PageSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import * as cagregorian from './ca-gregorian.json';
import * as currencies from './currencies.json';
import { formatData } from './datasource';
import * as numberingSystems from './numberingSystems.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(currencies, cagregorian, numbers, timeZoneNames, numberingSystems);

setCulture('de');
setCurrencyCode('EUR');

L10n.load({
    'de-DE': {
        'pager': {
            'currentPageInfo': '{0} von {1} Seiten',
            'firstPageTooltip': 'Zur ersten Seite',
            'lastPageTooltip': 'Zur letzten Seite',
            'nextPageTooltip': 'Zur nächsten Seite',
            'nextPagerTooltip': 'Zum nächsten Pager',
            'previousPageTooltip': 'Zurück zur letzten Seit',
            'previousPagerTooltip': 'Zum vorherigen Pager',
            'totalItemsInfo': '({0} Beiträge)'
        },
        'treegrid': {
            "ClearButton": "klar",
            'Collapse All': 'Alles einklappen',
            "Contains": "Enthält",
            'EmptyRecord': 'Keine Aufzeichnungen angezeigt',
            "EndsWith": "Endet mit",
            "EnterValue": "Geben Sie den Wert ein",
            "Equal": "Gleich",
            "Excelexport": "Excel-Export",
            'Expand All': 'Alle erweitern',
            "FilterButton": "Filter",
            "FilterMenu": "Filter",
            "GreaterThan": "Größer als",
            "GreaterThanOrEqual": "Größer als oder gleich",
            "LessThan": "Weniger als",
            "LessThanOrEqual": "Weniger als oder gleich",
            "NotEqual": "Nicht gleich",
            "Pdfexport": "PDF-Export",
            "Print": "Drucken",
            "StartsWith": "Beginnt mit",
            "Wordexport": "Word-Export"
        }
    }
});

export default class App extends React.Component<{}, {}>{

    public FilterOptions: FilterSettingsModel = {
        type: 'Menu'
    };
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public toolbarOptions: ToolbarItems[] = ['Print'];

    public formatOption : object = {
        currency:'EUR',
        format:'C2',
        maximumSignificantDigits:3,
        minimumSignificantDigits:1,
        useGrouping: false
    };


    public render() {
        return <TreeGridComponent dataSource={formatData} treeColumnIndex={1} childMapping='subtasks' allowPaging='true' pageSettings={this.pageSettings} locale='de-DE' allowFiltering='true'
        filterSettings={this.FilterOptions} toolbar={this.toolbarOptions} height='220'>
            <ColumnsDirective>
              <ColumnDirective field='orderID' headerText='Order ID' width='90' textAlign='Right'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='180'/>
              <ColumnDirective field='price' headerText='Price' width='80' format={this.formatOption} textAlign='Right' type='number' />
            </ColumnsDirective>
            <Inject services={[Page, Filter, Toolbar]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> * In the above sample, *Price* column is formatted by **NumberFormatOptions**.
> * By default, [`locale`](../api/treegrid/#locale) value is *en-US*. If you want to change the *en-US* culture to a different culture, you have to change  the [`locale`](../api/treegrid/#locale) accordingly.

## Right to left (RTL)

RTL provides an option to switch the text direction and layout of the TreeGrid component from right to left. It improves the user experiences and accessibility for users who use right-to-left languages (Arabic, Farsi, Urdu, etc.). To enable RTL Grid, set the [`enableRtl`](../api/treegrid/#enablertl) to **true**.

{% tab template="treegrid/internationalization", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Filter, FilterSettingsModel, Inject, PageSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

L10n.load({
    'ar-AE': {
        'pager': {
            'currentPageInfo': '{0} من {1} صفحة',
            'firstPageTooltip': 'انتقل إلى الصفحة الأولى',
            'lastPageTooltip': 'انتقل إلى الصفحة الأخيرة',
            'nextPageTooltip': 'انتقل إلى الصفحة التالية',
            'nextPagerTooltip': 'الذهاب إلى بيجر المقبل',
            'previousPageTooltip': 'انتقل إلى الصفحة السابقة',
            'previousPagerTooltip': 'الذهاب إلى بيجر السابقة',
            'totalItemsInfo': '({0} العناصر)'
        },
        'treegrid': {
            "ChooseDate": "اختر تاريخا",
            "ClearButton": "واضح",
            "Contains": "يحتوي على",
            "EmptyRecord": "لا سجلات لعرضها",
            "EndsWith": "ينتهي مع",
            "EnterValue": "أدخل القيمة",
            "Equal": "مساو",
            "FilterButton": "منقي",
            "FilterMenu": "منقي",
            "GreaterThan": "أكثر من",
            "GreaterThanOrEqual": "أكبر من أو يساوي",
            "LessThan": "أقل من",
            "LessThanOrEqual": "اصغر من او يساوي",
            "NotEqual": "غير متساوي",
            "Print": "طباعة",
            "StartsWith": "ابدا ب",
        }
    }
});

export default class App extends React.Component<{}, {}>{

    public FilterOptions: FilterSettingsModel = {
        type: 'Menu'
    };
    public pageSettings: PageSettingsModel = { pageSize: 7 };
    public toolbarOptions: ToolbarItems[] = ['Print'];

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
        allowPaging='true' pageSettings={this.pageSettings} locale='ar-AE' allowFiltering='true'
        filterSettings={this.FilterOptions} toolbar={this.toolbarOptions} enableRtl= {true} height='220'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='160'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page, Toolbar, Filter]}/>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## See Also

* [Internationalization](../common/internationalization)
* [Localization](../common/localization)