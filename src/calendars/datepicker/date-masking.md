---
title: "Date Masking"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Enable the Masked Input

DatePicker has `enableMask` property that provides the option to enable the built-in date masking support. Also, you must inject the MaskedDateTime module to enable the masking support.

{% tab template="datepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { DatePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public render() {
        return <DatePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></DatePickerComponent>
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

The mask pattern is defined based on the provided date format to the component. If the format is not specified, the mask pattern is formed based on the default format of the current culture.

| **Keys** | **Actions** |
| --- | --- |
| <kbd>Up / Down arrows</kbd> | To increment and decrement the selected portion of the date. |
| <kbd>Left / Right arrows and Tab</kbd> | To navigate the selection from one portion to next portion |

The following example demonstrates default and custom format of DatePicker component with mask.

{% tab template="datepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { DatePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public render() {
       return (
            <div>
                {/* specifies the masked DatePicker component without format */}
                <DatePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></DatePickerComponent>
                <br />
                <br />

                {/* specifies the masked DatePicker component with format  */}
                <DatePickerComponent format='dd-MM-yyyy' enableMask={true}><Inject services={[MaskedDateTime]} /></DatePickerComponent>
            </div>
        );

    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

# Configure Mask Placeholder

You can change mask placeholder value through property `maskPlaceholder`. By default , it takes the full name of date and time co-ordinates such as `day`, `month`, `year`, `hour` etc.

While changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through load method of L10n class for mask placeholder values like below.

```typescript
//Load the L10n from ej2-base
import { L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized mask placeholder value
L10n.load({
'de': {
    datepicker: { day: 'Tag' , month: 'Monat', year: 'Jahr' }
}
});

```

The following example demonstrates default and customized mask placeholder value.

{% tab template="datepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { DatePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    private maskPlaceholderValue: object;
    constructor(props: {}) {
    super(props);
    this.maskPlaceholderValue = {day: 'd', month: 'M', year: 'y'};
    }
    public render() {
       return (
            <div>
                {/* specifies the masked DatePicker component without mask placeholder */}
                <DatePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></DatePickerComponent>
                <br />
                <br />

                {/* specifies the masked DatePicker component with mask placeholder  */}
                <DatePickerComponent  enableMask={true} maskPlaceholder={this.maskPlaceholderValue}><Inject services={[MaskedDateTime]} /></DatePickerComponent>
            </div>
        );

    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
