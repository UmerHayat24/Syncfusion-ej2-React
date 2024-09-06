---
title: "Autocomplete Localization"
component: "AutoComplete"
description: "This section explains the localization support of Syncfusion react autocomplete component."
---

# Localization

The Localization library allows you to localize the static text content of
[noRecordsTemplate](../api/auto-complete/#norecordstemplate) and [actionFailureTemplate](../api/auto-complete/#actionfailuretemplate)
&nbsp;properties according to the culture currently assigned to the AutoComplete.

| Locale key | en-US (default)  |
|------|------|
| noRecordsTemplate |  No Records Found |
| actionFailureTemplate | The Request Failed |

## Loading translations

To load translation object to your application, use load function of the **L10n** class.

In the following sample, French culture is set to the AutoComplete and no data is loaded. Hence,the
`noRecordsTemplate` property displays its text in French culture initially, and if the sample is run offline,
 then the `actionFailureTemplate` property  displays its text appropriately.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
// import L10n class for load function
import { L10n } from '@syncfusion/ej2-base';
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind remotedata to showcase actionFailureTemplate in offline.
    private customerData: DataManager = new DataManager({
      adaptor: new ODataV4Adaptor,
      crossDomain: true,
      url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers'
    });

    // maps the appropriate column to fields property
    private fields: object = { value: 'ContactName' };

    // take 0 item to showcase noRecordsTemplate property.
    private query: Query = new Query().select(['ContactName', 'CustomerID']).take(0);

    // set locale culture to AutoComplete
    public componentWillMount() {
        L10n.load({
            'fr-BE': {
                'dropdowns': {
                  'actionFailureTemplate': "Modèle d'échec d'action",
                    'noRecordsTemplate': "Aucun enregistrement trouvé",
                }
            }
        });
    }

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" fields={this.fields} locale="fr-BE" query={this.query} dataSource={this.customerData} placeholder="Trouver un client"/>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [Accessibility](./accessibility/)
* [How to bind the data to the autocomplete](./data-binding/)