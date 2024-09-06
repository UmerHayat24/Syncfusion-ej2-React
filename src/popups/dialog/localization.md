---
title: "Localization"
component: "Dialog"
description: "Explains how to localize the static text (built-in text) content of the dialog control such as close button's tooltip text."
---

# Localization

[Localization](/base/localization.html) library allows to localize the default text content of
Dialog. In Dialog, The close button's tooltip text alone will be localize based on culture.

| Locale key | en-US (default)  |
|------|------|
| close |  Close |

## Loading translations

To load translation object in an application use `load` function of `L10n` class.

In the below sample, `French` culture is set to Dialog and change the close button's tooltip
text.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript
import { L10n } from '@syncfusion/ej2-base';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

// Load French culture for Dialog close button tooltip text
L10n.load({
  'fr-BE': {
     'dialog': {
           'close': "Fermer"
       }
   }
});

class App extends React.Component<{}, {}> {
  public content = (): JSX.Element => {
      return (
        <div>
        Dialogue avec la culture française
        </div>
      )
  }
  public render() {
    return (
      <div className="App" id='dialog-target'>
    <DialogComponent
    width='250px' locale= 'fr-BE' content={this.content} header='Dialog' closeOnEscape={false}
    showCloseIcon={true} target='#dialog-target'/>
      </div>
  );
  }
}
export default App;

```

{% endtab %}
