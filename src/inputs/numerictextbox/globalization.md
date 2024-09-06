---
title: "Globalization"
component: "NumericTextBox"
description: "Globalization support in numeric textbox"
---

# Globalization

## Localization

[`Localization`](../common/localization/) library allows users to localize the default text contents
of the NumericTextBox to different cultures using the [`locale`](../api/numerictextbox#locale) property.
In NumericTextBox, spin buttons title for the tooltip will be localized based on the culture.

| Locale key | en-US (default)  |
|------|------|
| incrementTitle |  Increment value |
| decrementTitle |  Decrement value |

### Loading translations

To load translation object in your application use `load` function of `L10n` class.

The below example demonstrates the NumericTextBox in `German` culture with the spin buttons tooltip.

{% tab template="numeric-textbox/getting-started", sourceFiles="app/**/*.tsx" %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

L10n.load({
    'de': {
      'numerictextbox': { incrementTitle: 'Wert erhöhen', decrementTitle: 'Dekrementwert'}
    }
});

// initializes NumericTextBox component
// sets `German` culture using the culture value 'de'
ReactDOM.render(<NumericTextBoxComponent locale='de' value={10} />,document.getElementById('numericContainer'));

```

{% endtab %}

## Internationalization

Internationalization library provides support for formatting and parsing the number by using the
official [Unicode CLDR](http://cldr.unicode.org/) JSON data and also provides the
`loadCldr` method to load the culture specific CLDR JSON data. The NumericTextBox comes with built-in
internationalization support to adapt based on culture. For more information about internationalization,
refer to this [link](../common/internationalization/).

By default, all the Essential JS 2  component are specific to English culture ('en-US').
If you want to go with the different culture other than `English`, follow the below steps.

* Install the `CLDR-Data` package by using the below command (it installs the CLDR JSON data). For more information about CLDR-Data,
refer to this [link](http://cldr.unicode.org/index/cldr-spec/json).

```cmd
npm install cldr-data --save
```

Once the package installed, you can find the culture
specific JSON data under the location `\node_modules\cldr-data`.

* Now import the installed CLDR JSON data into the `app.tsx` file.

* Now import the required culture
from the installed location to `app.tsx` file as like the below code snippets.

```typescript
import * as currencies from 'cldr-data/main/de/currencies.json';
import * as numbers from 'cldr-data/main/de/numbers.json';
import * as currencyData from 'cldr-data/supplemental/currencyData.json';
import * as numberingSystems from 'cldr-data/supplemental/numberingSystems.json';

loadCldr(numberingSystems, currencies, numbers, currencyData);
```

> if you are facing the error `/node_modules/cldr-data/main/de/*.json (1,1): unused expression, expected an assignment or function call` when you are adding the json files to render the culture sample, then add the below configuration in your `tslint.json` file

```typescript

"linterOptions": {
    "exclude": [
      "*.json",
      "**/*.json"
    ]
  }

```

* Set the culture by using the [`locale`](../api/numerictextbox#locale) property.

The below example demonstrates the NumericTextBox in `German` culture with the `EUR` currency format.

{% tab template="numeric-textbox/internationalization" , isDefaultActive = "true" , sourceFiles="app/**/*.tsx" %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { loadCldr,L10n } from '@syncfusion/ej2-base';
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as currencyData from './currencyData.json';
import * as numbers from './numbers.json';
import * as currencies from './currencies.json';

loadCldr(numberingSystems, currencyData, numbers, currencies);

L10n.load({
    'de': {
      'numerictextbox': { incrementTitle: 'Wert erhöhen', decrementTitle: 'Dekrementwert'}
    }
});

// initializes NumericTextBox component
// sets `German` culture using the culture value 'de'
// sets the 'EUR' currency format
ReactDOM.render(<NumericTextBoxComponent locale='de' currency='EUR' format='c2' value={100} >
</NumericTextBoxComponent>,document.getElementById('numericContainer'));

```

{% endtab %}

## Right to Left(RTL)

RTL provides an option to switch the text direction and layout of the NumericTextBox component from right to left. It improves the user experiences and accessibility for users who use right-to-left languages (Arabic, Farsi, Urdu, etc.). To enable RTL NumericTextBox, set the [`enableRtl`](../api/numerictextbox#enablertl) to true.

{% tab template="numeric-textbox/rtl" , isDefaultActive = "true" , sourceFiles="app/**/*.tsx" %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { loadCldr,L10n } from '@syncfusion/ej2-base';

L10n.load({
    'ar-AE': {
      'numerictextbox': { incrementTitle: 'قيمة الزيادة', decrementTitle: 'قيمة تناقص'}
    }
});

// initializes NumericTextBox component
// sets `German` culture using the culture value 'de'
// sets the 'EUR' currency format
ReactDOM.render(<NumericTextBoxComponent locale='ar-AE' enableRtl='true' floatLabelType='Auto' placeholder='أدخل القيمة' value={100} >
</NumericTextBoxComponent>,document.getElementById('numericContainer'));

```

{% endtab %}
