---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Render Calendar with week number

You can enable the `weekNumber` in Calendar by using the
[`weekNumber`](../../api/calendar#weeknumber)
property.

{% tab template="calendar/default", sourceFiles="app/**/*.tsx" %}

```typescript
// import the calendarcomponent
import { CalendarComponent} from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        return <CalendarComponent id="calendar" weekNumber={true} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}