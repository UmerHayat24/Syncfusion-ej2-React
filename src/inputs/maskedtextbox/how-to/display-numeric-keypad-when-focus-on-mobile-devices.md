# Display numeric keypad when focus on mobile devices

By default, on focusing the MaskedTextBox, alphanumeric keypad will be displayed on
mobile devices. Sometimes only numeric keypad for number
values is needed, and this can be achieved by setting "type" property to `tel`.
Refer to the following example to enable numeric keypad in MaskedTextBox.

{% tab template="masked-textbox/cursor-position-any", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
import { MaskedTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public render() {
      return (
        <div>
          <br/><MaskedTextBoxComponent name="mask_value" mask='999-99999' value= "342-45432" type="tel"/>
        </div>
      );
  }
};
ReactDOM.render(<App />, document.getElementById('masktextbox'));

```

{% endtab %}