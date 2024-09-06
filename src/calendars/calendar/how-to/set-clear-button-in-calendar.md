---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Set clear button

The following steps illustrate how to configure clear button in Calendar UI.

* On [`created`](../../api/calendar#created)
event of Calendar add the required
elements to have clear button.
Here we have used div with Essential JS 2 Button component.

* Use the `e-footer` class to the div tag to act as the footer.

* And use the button to clear the selected date.

* Bind the required event handler to the button tags to update the value.

Below is the code example

{% tab template="calendar/how-to", sourceFiles="app/**/*.tsx" %}

```typescript
// import the calendarcomponent
import { CalendarComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    public onCreated(): void {
        const proxy: any = this;
        const clearBtn = document.createElement('button');
        clearBtn.setAttribute('class', 'e-btn e-clear e-flat');
        clearBtn.innerHTML = 'Clear';
        const footerElement: HTMLElement = document.querySelector('.e-footer-container') as HTMLElement;
        footerElement.insertBefore(clearBtn,footerElement.childNodes[0]);
        (document.querySelector(".e-clear") as HTMLElement).addEventListener("click",(e) => {
            proxy.value = null;
        });
    }
    public render() {
        return (
            <CalendarComponent id="calendar" created={this.onCreated} />
        );
     }
 }

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}