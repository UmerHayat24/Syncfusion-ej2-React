---
title: "Multiselect Localization"
component: "MultiSelect"
description: "This section explains the localization support of Syncfusion react multiselect component."
---

# Localization

The Localization library allows you to localize static text content of the
[noRecordsTemplate](../api/multi-select/#norecordstemplate)
 and [actionFailureTemplate](../api/multi-select/#actionfailuretemplate)
&nbsp;properties according to the culture currently assigned to the MultiSelect.

| Locale key | en-US (default)  |
|------|------|
| noRecordsTemplate |  No records found |
| actionFailureTemplate | The request failed |

## Loading translations

To load translation object to your application, use load function of the **L10n** class.

In the following sample, French culture is set to the MultiSelect and no data is loaded. Hence, the `noRecordsTemplate`
property displays its text in French culture initially, and if the sample is run offline, the `actionFailureTemplate` property
displays its text appropriately.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

// import L10n class for load function
import { L10n } from '@syncfusion/ej2-base';
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private fields: object = { text: 'ContactName', value: 'CustomerID' };

    // take 0 item to showcase noRecordsTemplate property.
    private query: Query = new Query().select(['ContactName', 'CustomerID']).take(0);

    // set locale culture to MultiSelect
    public componentWillMount() {
        L10n.load({
            'fr-BE': {
                'multi-select': {
                    'actionFailureTemplate': "Modèle d'échec d'action",
                    'noRecordsTemplate': "Aucun enregistrement trouvé"
                }
            }
        });
    }

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" fields={this.fields} locale="fr-BE" query={this.query} dataSource={this.customerData} placeholder="Sélectionnez un client" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [Accessibility](./accessibility/)
* [How to bind the data to the combobox](./data-binding/)