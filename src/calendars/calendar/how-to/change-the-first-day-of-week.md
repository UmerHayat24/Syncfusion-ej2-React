---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Change the first day of week

The Calendar provides an option to change the first day of the week by using the
[`firstDayOfWeek`](../../api/calendar#firstdayofweek)
property.
Day of the week starts from 0(Sunday) to 6(Saturday).

> By default, the first day of week is based on culture specific.

The following example demonstrates the Calendar with `Tuesday` as first day of the week.

{% tab template="calendar/default", sourceFiles="app/**/*.tsx" %}

```typescript
// import the calendarcomponent
import { CalendarComponent} from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    private weekstart:number = 2;

    public render() {
        return <CalendarComponent id="calendar" firstDayOfWeek={this.weekstart} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}