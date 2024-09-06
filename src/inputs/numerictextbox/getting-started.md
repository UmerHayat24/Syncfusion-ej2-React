---
title: "Getting Started"
component: "NumericTextBox"
description: "Rendering numeric textbox using React"
---

# Getting Started

The following section explains the required steps to build the
NumericTextBox component with its basic usage in step by step procedure.

## Dependencies

The following list of dependencies are required to use the NumericTextBox component in your application.

```javascript
|-- @syncfusion/ej2-react-inputs
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-react-base
```

## Installation and configuration

You can use [Create-react-app](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

```bash

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [npmjs.com](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install. For this application, we are going to use NumericTextBox component.

To install NumericTextBox component, use the following command

```bash
npm install @syncfusion/ej2-react-inputs –save
```

## Adding NumericTextBox to the application

Now, you can start adding NumericTextBox component to the application. We have added NumericTextBox component in `src/App.tsx`
file using following code.

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets value to the NumericTextBox
ReactDOM.render(<NumericTextBoxComponent value={10} /> ,document.getElementById('numericContainer'));

```

## Adding CSS reference

Import the NumericTextBox component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-inputs/styles/material.css";
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://ej2crg.azurewebsites.net/) (Custom Resource Generator) in your application.

## Run the application

Now use the `npm run start` command to run the application in the browser.

```cmd
npm run start
```

The below example shows the NumericTextBox.

{% tab template="numeric-textbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets value to the NumericTextBox
ReactDOM.render(<NumericTextBoxComponent value={10} />, document.getElementById('numericContainer'));

```

{% endtab %}

## Range validation

You can set the minimum and maximum range of values in the NumericTextBox using the [`min`](../api/numerictextbox#min) and
[`max`](../api/numerictextbox#max) properties, so the numeric value should be in the min and max range.

The validation behavior depends on the [`strictMode`](../api/numerictextbox#strictmode) property.

{% tab template="numeric-textbox/getting-started", sourceFiles="app/**/*.tsx" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets the minimum and maximum range values
// strictMode has been enabled by defualt
ReactDOM.render(<NumericTextBoxComponent min={10} max={20} value={16} step={2} />
  ,document.getElementById('numericContainer'));

```

{% endtab %}

## Formatting the value

User can set the format of the NumericTextBox component using [`format`](../api/numerictextbox#format)
property. The value will be displayed in the specified format, when the component is in focused out state. For more information about
formatting the value, refer to this [link](./formats/).

The below example demonstrates format the value by using currency format value `c2`.

{% tab template="numeric-textbox/getting-started", sourceFiles="app/**/*.tsx" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// sets currency with 2 numbers of decimal places format
ReactDOM.render(<NumericTextBoxComponent format='c2' value={10} />
,document.getElementById('numericContainer'));

```

{% endtab %}

## Precision of numbers

You can restrict the number of decimals to be entered in the NumericTextBox by using the [`decimals`](../api/numerictextbox#decimals)
and [`validateDecimalOnType`](../api/numerictextbox#validatedecimalontype) properties.
So, you can't enter the number whose precision is greater than the mentioned decimals.

* If `validateDecimalOnType` is false, number of decimals will not be restricted.
Else, number of decimals will be restricted while typing in the NumericTextBox.

{% tab template="numeric-textbox/precision", sourceFiles="app/**/*.tsx" %}

```typescript
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// initializes NumericTextBox component
// restricts number of decimals to be entered in the NumericTextBox by enabling validateDecimalOnType property
// sets number of decimal places to be allowed by the NumericTextBox
// sets number with 3 numbers of decimal places format
ReactDOM.render(<NumericTextBoxComponent validateDecimalOnType={true} decimals={3} format='n3' value={10} placeholder='ValidateDecimalOnType Enabled' floatLabelType='Auto' />
,document.getElementById('numericContainer1'));

// initializes NumericTextBox component
// validateDecimalOnType is false by default. So, number of decimals will not be restricted.
// sets number of decimal places to be allowed by the NumericTextBox
// sets number with 3 numbers of decimal places format
ReactDOM.render(<NumericTextBoxComponent decimals={3} format='n3' value={10} placeholder='ValidateDecimalOnType Disabled' floatLabelType='Auto' /> ,document.getElementById('numericContainer2'));
```

{% endtab %}

## See Also

* [How to perform custom validation using FormValidator](./how-to/perform-custom-validation-using-form-validator/)
* [How to customize the UI appearance of the control](./how-to/customize-the-ui-appearance-of-the-control/)
* [How to customize the spin button’s up and down arrow](./how-to/customize-the-spin-buttons-up-and-down-arrow/)
* [How to customize the step value and hide spin buttons](./how-to/customize-the-step-value-and-hide-spin-buttons/)
* [How to prevent nullable input in NumericTextBox](./how-to/prevent-nullable-input-in-numerictextbox/)
* [How to maintain trailing zeros in NumericTextBox](./how-to/maintain-trailing-zeros-in-numerictextbox/)