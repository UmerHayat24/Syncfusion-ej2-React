---
title: "How To"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the date time picker"
---

# Disable the component

To disable the DateTimePicker, use its
[`enable`](../../api/datetimepicker#enabled)
property to `false`.

{% tab template="datetimepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    private enable:boolean=false;

    public render() {
        return <DateTimePickerComponent id="datetimepicker" enabled={this.enable} placeholder='Select a date and time' />;
    }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}