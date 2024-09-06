---
title: "Accessibility"
component: "TimePicker"
description: "Time picker component support accessibility that helps to access all the features through the keyboard, on-screen readers, or other assertive technology devices."
---

# Accessibility

The web accessibility makes web applications and its content more accessible to people with disabled
without any barriers. Especially
it tracks the dynamic value changes and DOM changes.

TimePicker component has covered the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices)
specifications with the following list of WAI-ARIA
attributes `aria-haspopup`, `aria-selected`, `aria-disabled`, `aria-activedescendant`,
`aria-expanded`, `aria-owns`, and `aria-autocomplete`.

Here, the `combobox` as a role for input element and `listbox` as a role for popup element in the TimePicker.

* **Aria-haspopup** : Provides the information about whether this element display a pop-up window or not.

* **Aria-selected** : Indicates the current selected value of the TimePicker component.

* **Aria-disabled** : Indicates disabled state of the TimePicker component.

* **Aria-expanded** : Indicates expanded state of the popup.

* **Aria-autocomplete** : Indicates whether user input completion suggestions are provided or not.

* **Aria-owns** : Attribute that creates a parent/child relationship between the two DOM element in accessibility layer

* **Aria-activedescendent** : Attribute that helps in managing the current active child of the TimePicker component.

* **Role** : Attributes that gives assistive technologies information for handling each element in a widget.

## Keyboard Interaction

Keyboard accessibility is one of the most important aspects of web accessibility. It will be more useful to
all the computer users, as they often allow to interact keyboard more than a mouse.
Among people with disabilities like blind or who have motor disabilities are also can make frequent use of keyboard shortcuts.

The TimePicker component has built-in keyboard accessibility support by following the
[WAI-ARIA practices](http://www.w3.org/WAI/PF/aria-practices).

> It supports the following list of shortcut keys to interact with the TimePicker component.

| **Press** | **To do this** |
| --- | --- |
| <kbd>Upper Arrow</kbd> | Navigate and select the previous item. |
| <kbd>Down Arrow</kbd> | Navigate and select the next item. |
| <kbd>Left Arrow</kbd> | Move the cursor towards arrow key pressed direction. |
| <kbd>Right Arrow</kbd> | Move the cursor towards arrow key pressed direction. |
| <kbd>Home</kbd> | Navigate and select the first item. |
| <kbd>End</kbd> | Navigate and select the last item. |
| <kbd>Enter</kbd> | Select the currently focused item and close the popup. |
| <kbd>Alt + Upper Arrow</kbd> | Close the popup. |
| <kbd>Alt + Down Arrow</kbd> | Open the popup. |
| <kbd>Esc</kbd> | Close the popup. |

The following sample use the `alt+t` keys to focus the TimePicker component.

{% tab template="timepicker/keyboard", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

// import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
// import the timepicker
import { TimePicker, TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {

    private timepickerInstance: TimePicker;

    public componentDidMount() {
        const proxy = this;
        document.onkeyup = (e) => {
            if (e.altKey && e.keyCode === 84 /* t */) {
                // press alt+t to focus the control.
                 proxy.timepickerInstance.focus();
            }
        };
    }

    public render() {
        return <TimePickerComponent id="timepicker" placeholder="Select a Time" ref={(scope) => { (this.timepickerInstance as TimePicker | null)  = scope; }}/>
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));

```

{% endtab %}