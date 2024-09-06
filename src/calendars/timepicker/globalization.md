---
title: "Globalization"
component: "TimePicker"
description: "Learn about how to globalize the time picker component and how to localize the culture related content."
---

# Globalization

Globalization is the combination of internationalization and localization. You can adapt the component to
various languages by means of parsing and formatting the date or
number [`internationalization`](../common/internationalization/) , and also add
culture specific customization and translation to the text
[`localization`](../common/localization/).

By default, TimePicker time format and meridian names are specific to the `American English` culture. It utilizes the
[`Essential JavaScript 2 Internationalization`](../common/internationalization)
package to parse and format the date object based on the culture by using the official [`UNICODE CLDR`](http://cldr.unicode.org/)
JSON data. It provides the `loadCldr` method to load culture specific CLDR JSON data. To go with the different culture other
than `English`, follow the steps below.

* Install the `CLDR-Data` package by using the following command (it installs all the CLDR JSON data). To
known more about CLDR-Data refer the [`CLDR-Data`](http://cldr.unicode.org/index/cldr-spec/json) link.

```cmd
npm install cldr-data --save
```

 Once the package is installed, you can find the culture
specific JSON data under the location `\node_modules\cldr-data`.

* Import the installed CLDR JSON data into the `app.ts` file.

* Use the [`loadCldr`](../common/internationalization#cldr-data-dependencies)
method
to load the culture specific CLDR JSON data
from the installed location to `app.ts` file.

* TimePicker displayed `Sunday` as the first day of week based on default culture ("en-US"). If you want to display the TimePicker with loaded culture’s first day of week, you need to import `weekdata.json` file from the `cldr-data/suppemental` as given in the code example.

```typescript

import { loadCldr } from '@syncfusion/ej2-base';

import { loadCldr } from "@syncfusion/ej2-base";

import * as gregorian from 'cldr-data/main/de/ca-gregorian.json';
import * as numbers from 'cldr-data/main/de/numbers.json';
import * as numberingSystems from 'cldr-data/supplemental/numberingSystems.json';

loadCldr(numberingSystems, gregorian, numbers);
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

* Before changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through `load` method of `L10n` class.

```typescript

//Load the L10n, loadCldr from ej2-base
import { loadCldr, L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized placeholder value
L10n.load({
    'de': {
        'timepicker': { placeholder: 'Wählen Sie Zeit'}
    }
});

```

* Set the culture by using the
[`locale`](../api/timepicker#locale)
property. In the following code example, the DateTimePicker is initialized
in `German` culture with
corresponding localized text.

The following example demonstrates the TimePicker in `German` culture.

{% tab template="timepicker/internationalization", isDefaultActive = "true",sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";
//Load the L10n, loadCldr from ej2-base
import { loadCldr, L10n } from '@syncfusion/ej2-base';
//import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
//import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';

// enable ripple effect
enableRipple(true);

//load the CLDR data files.
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';

loadCldr(numberingSystems, gregorian, numbers);

L10n.load({
    'de': {
        'timepicker': { placeholder: 'Wählen Sie Zeit' }
    }
});
//import the timepickercomponent
class App extends React.Component<{}, {}> {
    render() {
        return <TimePickerComponent id="time" locale='de'/>
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));


```

{% endtab %}

## Right-To-Left

The TimePicker supports RTL (right-to-left) functionality for languages like Arabic and Hebrew to displays the
text in the right-to-left direction. Use
[`enableRtl`](../api/timepicker#enablertl)
property to set the RTL direction.

The code example demonstrates the TimePicker component in `Arabic` culture, also explains how to set the localized text to
the placeholder using [`L10n.load`](http://ej2.syncfusion.com/documentation/base/api/l10n/) method.

{% tab template="timepicker/rtl",  sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";
//Load the L10n, loadCldr from ej2-base
import { loadCldr, L10n } from '@syncfusion/ej2-base';
//import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
//import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';

// enable ripple effect
enableRipple(true);

//load the CLDR data files.
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';

loadCldr(numberingSystems, gregorian, numbers);

L10n.load({
    'ar': {
        'timepicker': { placeholder: 'حدد الوقت' }
    }
});
//import the timepickercomponent
class App extends React.Component<{}, {}> {

    private rtl:boolean=true;

    render() {
        return <TimePickerComponent id="time" locale='ar' enableRtl={this.rtl} />
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));


```

{% endtab %}