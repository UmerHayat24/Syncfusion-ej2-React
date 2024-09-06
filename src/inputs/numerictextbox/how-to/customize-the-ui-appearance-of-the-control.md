# Customize the UI appearance of the control

You can change the appearance of the NumericTextBox by adding custom `cssClass` to the component and enabling styles. Refer to the following example to change the appearance of the NumericTextBox.

{% tab template="numeric-textbox/custom-css", sourceFiles="app/**/*.tsx,style.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';

// initializes NumericTextBox component
export default class App extends React.Component<{}, {}> {
  render() {
    return (
      <NumericTextBoxComponent id="sample" value={10} cssClass={'e-style'} placeholder="Enter value" floatLabelType={'Always'}/>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('numericContainer'));
```

{% endtab %}