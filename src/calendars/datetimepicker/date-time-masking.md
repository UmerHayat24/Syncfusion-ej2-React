---
title: "Date and Time masking"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the datetimepicker"
---

# Enable the Masked Input

DateTimePicker has `enableMask` property that provides the option to enable the built-in date masking support. Also, you must inject the MaskedDateTime module to enable the masking support.

{% tab template="datetimepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { DateTimePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public render() {
        return <DateTimePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></DateTimePickerComponent>
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

The mask pattern is defined based on the provided date format to the component. If the format is not specified, the mask pattern is formed based on the default format of the current culture.

| **Keys** | **Actions** |
| --- | --- |
| <kbd>Up / Down arrows</kbd> | To increment and decrement the selected portion of the date and time. |
| <kbd>Left / Right arrows and Tab</kbd> | To navigate the selection from one portion to next portion |

The following example demonstrates default and custom format of DateTimePicker component with mask.

{% tab template="datetimepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { DateTimePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public render() {
       return (
            <div>
                {/* specifies the masked DateTimePicker component without format */}
                <DateTimePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></DateTimePickerComponent>
                <br />
                <br />

                {/* specifies the masked DateTimePicker component with format  */}
                <DateTimePickerComponent format='dd-MM-yyyy hh:mm a' enableMask={true}><Inject services={[MaskedDateTime]} /></DateTimePickerComponent>
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
    datetimepicker: { day: 'Tag' , month: 'Monat', year: 'Jahr', hour: 'Stunde' ,minute: 'Minute', second:'Sekunden' }
}
});

```

The following example demonstrates default and customized mask placeholder value.

{% tab template="datetimepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { DateTimePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    private maskPlaceholderValue: object;
    constructor(props: {}) {
    super(props);
    this.maskPlaceholderValue = {day: 'd', month: 'M', year: 'y', hour: 'h', minute: 'm', second: 's'};
    }
    public render() {
       return (
            <div>
                {/* specifies the masked DateTimePicker component without mask placeholder */}
                <DateTimePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></DateTimePickerComponent>
                <br />
                <br />

                {/* specifies the masked DateTimePicker component with mask placeholder  */}
                <DateTimePickerComponent  enableMask={true} maskPlaceholder={this.maskPlaceholderValue}><Inject services={[MaskedDateTime]} /></DateTimePickerComponent>
            </div>
        );

    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
