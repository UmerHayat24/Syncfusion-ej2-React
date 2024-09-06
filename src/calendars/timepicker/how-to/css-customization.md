---
title: "How To"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the time picker"
---

# CSS customization

TimePicker allows you to customize the textbox and popup list appearance to suit for your
application by using
[`cssClass`](../../api/timepicker#cssclass) property.

The below sample demonstrates customization of the text appearance in a textbox, popup button, and popup list along with hover and active
state by using `e-custom-style` class. Following is the list of available classes used to customize the entire TimePicker component.

| **Class Name** | **Description** |
| --- | --- |
| e-time-wrapper | Applied to TimePicker wrapper element. |
| e-timepicker |  Applied to input element and TimePicker popup element. |
| e-time-wrapper.e-timepicker | Applied to input element only. |
| e-input-group-icon.e-time-icon | Applied to popup button. |
| e-float-text | Applied to floating label text element. |
| e-popup | Applied to popup element. |
| e-timepicker.e-popup | Applied to TimePicker popup element only. |
| e-list-parent | Applied to popup UL element. |
| e-timepicker.e-list-parent | Applied to TimePicker popup UL element only. |
| e-list-item | Applied to LI elements. |
| e-hover | Applied to LI element hovering time. |
| e-active | Applied to active LI element. |

{% tab template="timepicker/how-to", isDefaultActive = "true", sourceFiles="app/**/*.tsx,style.css" %}

```typescript

// import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
// import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {
    public render() {
        return <TimePickerComponent id="timepicker" cssClass="e-custom-style" placeholder="Select a Time" />
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));

```

{% endtab %}