---
title: "Formats"
component: "NumericTextBox"
description: "Custom formats in numeric textbox"
---

# Number Formats

You can format the value of NumericTextBox using [`format`](../api/numerictextbox#format) property.
The value will be displayed in the specified format when the component is in focused out state. The format string
supports both the [standard numeric format string](../common/internationalization#number-formatter-and-parser/)
and [custom numeric format string](../common/internationalization#custom-number-formatting-and-parsing/).

## Standard formats

From the [standard numeric formats](../common/internationalization#number-formatter-and-parser/), you can use the numeric related
format specifiers such as `n`,`p` and `c` in the NumericTextBox component. By using these format specifiers, you can achieve the percentage
and currency textbox behavior also.

The below example demonstrates percentage and currency formats.

{% tab template="numeric-textbox/standard-format", sourceFiles="app/**/*.tsx" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets percentage with 2 numbers of decimal places format
ReactDOM.render(<NumericTextBoxComponent format='p2' value={0.5} min={0} max={1} step={0.01} placeholder='Percentage format' floatLabelType='Auto' />
,document.getElementById('numericContainer1'));

// initializes NumericTextBox component
// sets currency with 2 numbers of decimal places format
ReactDOM.render(<NumericTextBoxComponent format='c2' value={10} placeholder='Currency format' floatLabelType='Auto' />
,document.getElementById('numericContainer2'));

```

{% endtab %}

## Custom formats

From the [custom numeric format string](../common/internationalization#custom-number-formatting-and-parsing/), you can provide any custom format by
combining one or more custom specifiers.

The below examples demonstrate format the value by using currency format string `#` and `0`.

{% tab template="numeric-textbox/custom-format", sourceFiles="app/**/*.tsx" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets the format using custom format string `#`
ReactDOM.render(<NumericTextBoxComponent format='###.##' value={10} placeholder='Custom format string #' floatLabelType='Auto'  />, document.getElementById('numericContainer1'));

// initializes NumericTextBox component
// sets the format using custom format string `0`
ReactDOM.render(<NumericTextBoxComponent format='000.00' value={10} placeholder='Custom format string 0' floatLabelType='Auto' />, document.getElementById('numericContainer2'));

```

{% endtab %}