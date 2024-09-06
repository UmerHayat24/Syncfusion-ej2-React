---
title: "Drop-down list Localization"
component: "DropDownList"
description: "This section explains the localization support of Syncfusion react drop-down list component."
---

# Localization

The Localization library allows you to localize static text content of the
[noRecordsTemplate](../api/drop-down-list/#norecordstemplate)
 and [actionFailureTemplate](../api/drop-down-list/#actionfailuretemplate)
&nbsp;properties according to the culture currently assigned to the DropDownList.

| Locale key | en-US (default)  |
|------|------|
| noRecordsTemplate |  No records found |
| actionFailureTemplate | The request failed |

## Loading translations

To load translation object to your application, use load function of the **L10n** class.

In the following sample, French culture is set to the DropDownList and no data is loaded. Hence, the
`noRecordsTemplate` property displays its text in French culture initially, and if the sample is run
offline, the `actionFailureTemplate` property displays its text appropriately.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
// import L10n class for load function
import { L10n } from '@syncfusion/ej2-base';
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
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

  // set locale culture to DropDownList
  public componentWillMount() {
    L10n.load({
      'fr-BE': {
        'dropdowns': {
          'actionFailureTemplate': "Modèle d'échec d'action",
          'noRecordsTemplate': "Aucun enregistrement trouvé"
        }
      }
    });
  }

  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" fields={this.fields} locale="fr-BE" query={this.query} dataSource={this.customerData} placeholder="Sélectionnez un client" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [Accessibility](./accessibility/)
* [How to bind the data to the combobox](./data-binding/)