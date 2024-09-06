---
title: "Calendar Views"
component: "Calendar"
description: "Pre-defined views in calendar allows to perform easy navigation to select any date."
---

# Calendar Views

The Calendar has the following predefined views
that provides a flexible way to navigate back and forth to select the date.
Use the
[`start`](../api/calendar#start)
property to change the default view of the Calendar.

| **View** | **Description** |
| --- | --- |
| month (default) | Displays the days in a month |
| year | Displays the months in a year |
| decade | Displays the years in a decade |

The following example demonstrates how to set the `year` as the start view of the calendar.

{% tab template="calendar/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the calendarcomponent
import { CalendarComponent} from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        //creates a calendar with decade view and navigate up to year view.
        return <CalendarComponent id="calendar" start='Year' />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## View Restriction

Calendar view can be restricted by defining the [`start`](../api/calendar#start)
  and [`depth`](../api/calendar#depth)

By defining the start and depth property with the different view, drill-
down and drill-up views navigation can be limited to the user. Calendar views will be drill-down up to the
view which is set in `depth` property and drill-up up to the view which is set in `start` property.

> Always the depth view has to be smaller than the start view.

{% tab template="calendar/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the calendarcomponent
import { CalendarComponent} from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        // creates a calendar with decade view and navigate up to year view.
        return <CalendarComponent id="calendar" start='Decade' depth='Year' />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

You can restrict the calendar's drill down navigation by defining the [`start`](../api/calendar#start)
  and [`depth`](../api/calendar#depth) property

The following example demonstrates how to select the date in `year` view.

{% tab template="calendar/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the calendarcomponent
import { CalendarComponent} from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        //creates a calendar with decade view and navigate up to year view.
        return <CalendarComponent id="calendar" start='Year' depth='Year' />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}