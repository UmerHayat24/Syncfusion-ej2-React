---
title: "Time masking"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the TimePicker"
---

# Enable the Masked Input

TimePicker has `enableMask` property that provides the option to enable the built-in date masking support. Also, you must inject the MaskedDateTime module to enable the masking support.

{% tab template="timepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { TimePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public render() {
        return <TimePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></TimePickerComponent>
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

The mask pattern is defined based on the provided time format to the component. If the format is not specified, the mask pattern is formed based on the default format of the current culture.

| **Keys** | **Actions** |
| --- | --- |
| <kbd>Up / Down arrows</kbd> | To increment and decrement the selected portion of the time. |
| <kbd>Left / Right arrows and Tab</kbd> | To navigate the selection from one portion to next portion |

The following example demonstrates default and custom format of TimePicker component with mask.

{% tab template="timepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { TimePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public render() {
       return (
            <div>
                {/* specifies the masked TimePicker component without format */}
                <TimePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></TimePickerComponent>
                <br />
                <br />

                {/* specifies the masked TimePicker component with format  */}
                <TimePickerComponent format='h:mm a' enableMask={true}><Inject services={[MaskedDateTime]} /></TimePickerComponent>
            </div>
        );

    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

# Configure Mask Placeholder

You can change mask placeholder value through property `maskPlaceholder`. By default , it takes the full name of  time co-ordinates such as `hour`, `minute` and `second`.

While changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through load method of L10n class for mask placeholder values like below.

```typescript
//Load the L10n from ej2-base
import { L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized mask placeholder value
L10n.load({
'de': {
    timepicker: { hour: 'Stunde' ,minute: 'Minute', second:'Sekunde' }
}
});

```

The following example demonstrates default and customized mask placeholder value.

{% tab template="timepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

import { TimePickerComponent, Inject, MaskedDateTime } from '@syncfusion/ej2-react-calendars';
import * as ReactDOM from 'react-dom';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    private maskPlaceholderValue: object;
    constructor(props: {}) {
    super(props);
    this.maskPlaceholderValue = { hour: 'h', minute: 'm', second: 's' };
    }
    public render() {
       return (
            <div>
                {/* specifies the masked TimePicker component without mask placeholder */}
                <TimePickerComponent enableMask={true}><Inject services={[MaskedDateTime]} /></TimePickerComponent>
                <br />
                <br />

                {/* specifies the masked TimePicker component with mask placeholder  */}
                <TimePickerComponent  enableMask={true} maskPlaceholder={this.maskPlaceholderValue}><Inject services={[MaskedDateTime]} /></TimePickerComponent>
            </div>
        );

    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
