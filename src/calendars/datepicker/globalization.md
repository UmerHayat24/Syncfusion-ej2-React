---
title: "Globalization"
component: "DatePicker"
description: "Learn about how to globalize the date picker component and how to localize the culture related content."
---

# Globalization

Globalization is the combination of internalization and localization. You can adapt the component to
various languages by parsing and formatting the date or
number [`Internationalization`](../common/internationalization/) and also add culture specific customization and translation to the text [`localization`](../common/localization/).

By default, DatePicker date format, week, and month names are specific to the `American English` culture. It utilizes the
[`Essential JavaScript 2 Internationalization`](../common/internationalization/)
package to parse and format the date object based on the culture by using the official [`UNICODE CLDR`](http://cldr.unicode.org/)
JSON data. It provides the `loadCldr` method to load culture specific CLDR JSON data. To use a different culture other
than `English`, follow the steps below:

* Install the `CLDR-Data` package by using the following command (installs all the CLDR JSON data). To know more about CLDR-Data refer to the [`CLDR-Data`](http://cldr.unicode.org/index/cldr-spec/json)link.

```cmd
npm install cldr-data --save
```

Once the package installed, you can find the culture
specific JSON data under the location `\node_modules\cldr-data`.

* Now import the installed CLDR JSON data into the `app.ts` file.

* Now use the
[`loadCldr`](http://ej2.syncfusion.com/documentation/base/internationalization#cldr-data-dependencies)
method
to load the culture specific CLDR JSON data
from the installed location to `app.ts` file.

* DatePicker displayed `Sunday` as the first day of week based on default culture ("en-US"). If you want to display the DatePicker with loaded culture’s first day of week, you need to import `weekdata.json` file from the `cldr-data/suppemental` as given in the code example.

```typescript

import { loadCldr } from "@syncfusion/ej2-base";

import * as gregorian from 'cldr-data/main/de/ca-gregorian.json';
import * as numbers from 'cldr-data/main/de/numbers.json';
import * as timeZoneNames from 'cldr-data/main/de/timeZoneNames.json';
import * as numberingSystems from 'cldr-data/supplemental/numberingSystems.json';
import * as weekData from 'cldr-data/supplemental/weekData.json';// To load the culture based first day of week

loadCldr(numberingSystems, gregorian, numbers, timeZoneNames, weekData);
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

> The `Localization` library allows you to localize default text content of the DatePicker. The DatePicker component has static text for  **today** feature that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/datepicker#locale) value and translation object.

Locale keywords |Text
-----|-----
today | Name of the button to choose Today date.
placeholder | Hint to describe expected value in input element.

* Before changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through `load` method of
  `L10n` class.

```typescript
//Load the L10n from ej2-base
import { L10n } from "@syncfusion/ej2-base";

//load the locale object to set the localized placeholder value
L10n.load({
  de: {
      datepicker: {
            placeholder: "Wählen Sie ein Datum",
            today:"heute"
        }
    }
});
```

* Set the culture by using the
[`locale`](../api/datepicker#locale)
property. The below code example, initialize
the DatePicker component in `German` culture with
corresponding localized text.

The following example demonstrates the DatePicker in `German` culture.

{% tab template="datepicker/globalization", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
// Load the L10n, loadCldr from ej2-base
import { loadCldr, L10n } from '@syncfusion/ej2-base';
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';

// load the CLDR data files.
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);

L10n.load({
    'de': {
        'datepicker': { placeholder: 'Wählen Sie ein Datum aus',
         today: 'heute' }
    }
});
// import the datepickercomponent
class App extends React.Component<{}, {}> {
    render() {
        return <DatePickerComponent id="datepicker" locale='de'/>;
    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Right-To-Left

The DatePicker supports right-to-left functionality for languages like Arabic, Hebrew to displays
the text in the right-to-left direction. Use
[`enableRtl`](../api/datepicker#enablertl)
property to set the RTL direction.

The below code example demonstrates the DatePicker component in `Hebrew` culture and
also explains how to set the localized text to
the placeholder using
[`load`](http://ej2.syncfusion.com/documentation/api/base/l10n#load)
 method of
[L10n](http://ej2.syncfusion.com/documentation/api/base/l10n/)
class.

{% tab template="datepicker/rtl", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
// Load the L10n, loadCldr from ej2-base
import { loadCldr, L10n } from '@syncfusion/ej2-base';
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';

// load the CLDR data files.
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);

L10n.load({
    'he': {
        'datepicker': { placeholder: 'הזן תאריך',
         today:'היום'
        }
    }
});
// import the datepickercomponent

class App extends React.Component<{}, {}> {

    render() {
        return <DatePickerComponent id="datepicker" locale='he' enableRtl={true} />;
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}