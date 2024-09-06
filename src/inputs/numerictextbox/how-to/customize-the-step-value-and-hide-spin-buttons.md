# Customize the step value and hide spin buttons

The spin buttons allow you to increase or decrease the value with the predefined [`step`](../../api/numerictextbox#step-number)
value. The visibility of spin buttons can be set using the[`showSpinButton`](../../api/numerictextbox#showspinbutton-boolean) property.

{% tab template="numeric-textbox/getting-started", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets the step value as '2' to increase/decrease the value by '2'
// sets the showSpinButton value as `false` to hide the spin buttons
ReactDOM.render(<NumericTextBoxComponent step={2} showSpinButton={false} min={10} max={100} value={16} />
,document.getElementById('numericContainer'));

```

{% endtab %}