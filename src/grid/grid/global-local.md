---
title: "Globalization"
component: "Grid"
description: "Learn how to apply localization (l10n), internationalization (i18n), and right-to-left (RTL) in Essential JS 2 DataGrid control."
---

# Globalization

## Localization

The [`Localization`](../../base/localization.html) library allows you to localize default text content of the Grid.
The grid component has static text on some features (like group drop area text, pager information text, etc.)
that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/grid/#locale) value and translation object.

The following list of properties and its values are used in the grid.

Locale key words |Text
-----|-----
EmptyRecord |No records to display
True |true
False |false
InvalidFilterMessage |Invalid Filter Data
GroupDropArea |Drag a column header here to group its column
UnGroup |Click here to ungroup
GroupDisable |Grouping is disabled for this column
FilterbarTitle |\s filter bar cell
EmptyDataSourceError |DataSource must not be empty at initial load since columns are generated from dataSource in AutoGenerate Column Grid
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
Columnchooser | Columns
Save | Save
Item | item
Items | items
EditOperationAlert | No records selected for edit operation
DeleteOperationAlert | No records selected for delete operation
SaveButton | Save
OKButton | OK
CancelButton | Cancel
EditFormTitle | Details of
AddFormTitle | Add New Record
BatchSaveConfirm | Are you sure you want to save changes?
BatchSaveLostChanges | Unsaved changes will be lost. Are you sure you want to continue?
ConfirmDelete | Are you sure you want to Delete Record?
CancelEdit | Are you sure you want to Cancel the changes?
ChooseColumns | Choose Column
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
Copy | Copy
Group | Group by this column
Ungroup | Ungroup by this column
autoFitAll | AutoFit all columns
autoFit | AutoFit this column
Export | Export
FirstPage | First Page
LastPage | Last Page
PreviousPage | Previous Page
NextPage | Next Page
SortAscending | Sort Ascending
SortDescending | Sort Descending
EditRecord | Edit Record
DeleteRecord | Delete Record
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
ShowRowsWhere | Show rows where
currentPageInfo | {0} of {1} pages
totalItemsInfo | ({0} items)
totalItemInfo | ({0} item)
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

To load translation object in an application use [`load`](https://ej2.syncfusion.com/documentation/api/base/l10n/#load) function of [`L10n`](https://ej2.syncfusion.com/documentation/api/base/l10n/) class.

The below example demonstrates the Grid in **Deutsch** culture.

{% tab template="grid/locale", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Group, Inject, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

L10n.load({
  'de-DE': {
      'grid': {
          'EmptyDataSourceError': 'DataSource darf bei der Erstauslastung nicht leer sein, da Spalten aus der dataSource im AutoGenerate Spaltenraster',
          'EmptyRecord': 'Keine Aufzeichnungen angezeigt',
          'GroupDropArea': 'Ziehen Sie einen Spaltenkopf hier, um die Gruppe ihre Spalte',
          'Item': 'Artikel',
          'Items': 'Artikel',
          'UnGroup': 'Klicken Sie hier, um die Gruppierung aufheben'
      },
      'pager':{
          'currentPageInfo': '{0} von {1} Seiten',
          'firstPageTooltip': 'Zur ersten Seite',
          'lastPageTooltip': 'Zur letzten Seite',
          'nextPageTooltip': 'Zur nächsten Seite',
          'nextPagerTooltip': 'Zum nächsten Pager',
          'previousPageTooltip': 'Zurück zur letzten Seit',
          'previousPagerTooltip': 'Zum vorherigen Pager',
          'totalItemsInfo': '({0} Beiträge)'
      }
  }
});

export default class App extends React.Component<{}, {}>{

public pageOptions : object = { pageSize: 6 };

  public render() {
    return <GridComponent  dataSource={data} locale='de-DE' allowPaging={true}
              pageSettings={this.pageOptions} allowGrouping={true}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
            </ColumnsDirective>
            <Inject services={[Page, Group]}/>
        </GridComponent>
    }
}
```

{% endtab %}

## Internationalization

The [`Internationalization`](../../base/internationalization.html) library is used to globalize number, date, and time values in grid component using format strings in the [`columns.format`](../api/grid/column/#format).

{% tab template="grid/internationalization", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { L10n, loadCldr, setCulture, setCurrencyCode } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Group, Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import * as cagregorian from './ca-gregorian.json';
import * as currencies from './currencies.json';
import { data } from './datasource';
import * as numberingSystems from './numberingSystems.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(currencies, cagregorian, numbers, timeZoneNames, numberingSystems);

const format : object = {  
  currency:'EUR',
  format:'C2',
  maximumSignificantDigits:3,
  minimumSignificantDigits:1,
  useGrouping: false
};

setCulture('de-DE');
setCurrencyCode('EUR');

L10n.load({
    'de-DE': {
        'grid': {
            'EmptyDataSourceError': 'DataSource darf bei der Erstauslastung nicht leer sein, da Spalten aus der dataSource im AutoGenerate Spaltenraster',
            'EmptyRecord': 'Keine Aufzeichnungen angezeigt',
            'GroupDropArea': 'Ziehen Sie einen Spaltenkopf hier, um die Gruppe ihre Spalte',
            'Item': 'Artikel',
            'Items': 'Artikel',
            'UnGroup': 'Klicken Sie hier, um die Gruppierung aufheben'
        },
        'pager':{
            'currentPageInfo': '{0} von {1} Seiten',
            'firstPageTooltip': 'Zur ersten Seite',
            'lastPageTooltip': 'Zur letzten Seite',
            'nextPageTooltip': 'Zur nächsten Seite',
            'nextPagerTooltip': 'Zum nächsten Pager',
            'previousPageTooltip': 'Zurück zur letzten Seit',
            'previousPagerTooltip': 'Zum vorherigen Pager',
            'totalItemsInfo': '({0} Beiträge)'
        }
    }
});

export default class App extends React.Component<{}, {}>{

    public pageOptions : PageSettingsModel = { pageSize: 6 };

    public render(){
      return <GridComponent  dataSource={data} locale='de-DE' allowPaging={true} allowGrouping={true}pageSettings={this.pageOptions}>
                <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                  <ColumnDirective field='Freight' headerText='Freight' width='150' format={format} textAlign="Right"/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page, Group]}/>
          </GridComponent>
    }
};
```

{% endtab %}

> * In the above sample, `Freight` column is formatted by `NumberFormatOptions`.
> * By default, [`locale`](../api/grid/#locale) value is `en-US`. If you want to change `en-US` culture, then set the [`locale`](../api/grid/#locale).

## Right to Left - RTL

RTL provides an option to switch the text direction and layout of Grid component from right to left.
It improves the user experiences and accessibility for users who use right-to-left languages(Arabic, Farsi, Urdu, etc).
To enable RTL in the Grid, set the [`enableRtl`](../api/grid/#enablertl) to **true**.

{% tab template="grid/locale", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


L10n.load({
  'ar-AE': {
      'grid': {
        'EmptyDataSourceError': 'يجب أن يكون مصدر البيانات فارغة في التحميل الأولي منذ يتم إنشاء الأعمدة من مصدر البيانات في أوتوجينيراتد عمود الشبكة',  
        'EmptyRecord': 'لا سجلات لعرضها'
      },
      'pager':{
          'currentPageInfo': '{0} من {1} صفحة',
          'firstPageTooltip': 'انتقل إلى الصفحة الأولى',
          'lastPageTooltip': 'انتقل إلى الصفحة الأخيرة',
          'nextPageTooltip': 'انتقل إلى الصفحة التالية',
          'nextPagerTooltip': 'الذهاب إلى بيجر المقبل',
          'previousPageTooltip': 'انتقل إلى الصفحة السابقة',
          'previousPagerTooltip': 'الذهاب إلى بيجر السابقة',
          'totalItemsInfo': '({0} العناصر)'
      }
  }
});

export default class App extends React.Component<{}, {}>{

public pageOptions : PageSettingsModel = { pageSize: 7 };

  public render() {
    return <GridComponent  dataSource={data} enableRtl= {true} locale='ar-AE' allowPaging={true} pageSettings={this.pageOptions}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
            <Inject services={[Page]}/>
        </GridComponent>
    }
};
```

{% endtab %}

## See Also

* [Internationalization](../../base/internationalization.html)
* [Localization](../../base/localization.html)
* [How to change left and right arrow traversing in React Grid](https://www.syncfusion.com/forums/162295/how-to-change-left-and-right-arrow-traversing-in-react-grid)