# Localization

Localization library allows you to localize the text content of the Syncfusion React component.

## Loading translations

To load a translation object in your application use [`load`](https://ej2.syncfusion.com/documentation/api/base/l10n#load) function of `L10n` class.

{% tab template="common/locale", sourceFiles="app/**/index.tsx", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { L10n } from '@syncfusion/ej2-base';
import { GridComponent, Inject, ColumnsDirective, ColumnDirective, Page, Group } from '@syncfusion/ej2-react-grids';
import { data } from './datasource';

L10n.load({
    'de-DE': {
        'grid': {
            'EmptyRecord': 'Keine Aufzeichnungen angezeigt',
            'GroupDropArea': 'Ziehen Sie einen Spaltenkopf hier, um die Gruppe ihre Spalte',
            'UnGroup': 'Klicken Sie hier, um die Gruppierung aufheben',
            'EmptyDataSourceError': 'DataSource darf bei der Erstauslastung nicht leer sein, da Spalten aus der dataSource im AutoGenerate Spaltenraster',
            'Item': 'Artikel',
            'Items': 'Artikel'
        },
        'pager':{
            'currentPageInfo': '{0} von {1} Seiten',
            'totalItemsInfo': '({0} Beiträge)',
            'firstPageTooltip': 'Zur ersten Seite',
            'lastPageTooltip': 'Zur letzten Seite',
            'nextPageTooltip': 'Zur nächsten Seite',
            'previousPageTooltip': 'Zurück zur letzten Seit',
            'nextPagerTooltip': 'Zum nächsten Pager',
            'previousPagerTooltip': 'Zum vorherigen Pager'
        }
    }
});

class App extends React.Component<{}, {}>{

public pageOptions : Object = { pageSize: 6 };

    render(){
        return <GridComponent  dataSource={data} locale='de-DE' allowPaging={true} pageSettings={this.pageOptions} allowGrouping={true}>
                  <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"></ColumnDirective>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'></ColumnDirective>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'></ColumnDirective>
                </ColumnsDirective>
                <Inject services={[Page, Group]}/>
            </GridComponent>
        }
};
ReactDOM.render(<App />, document.getElementById('grid'));

```

{% endtab %}

## Changing current locale

Current locale can be changed for all Syncfusion React components in your application by invoking
 `setCulture` function with your desired culture name.

{% tab compileJsx=true%}

```tsx

import {L10n, setCulture} from '@syncfusion/ej2-base';
L10n.load({
    'fr-BE': {
       'Grid': {
             'EmptyRecord': 'Aucun enregistrement à afficher',
             'InvalidFilterMessage':'Données de filtrage invalides',
              'UnGroup': 'Cliquez ici pour dégrouper '
         }
     }
});
setCulture('fr-BE');

```

{% endtab %}

> Note: Before changing a culture globally, you need to ensure that locale text for the concern culture is loaded through `L10n.load` function.
