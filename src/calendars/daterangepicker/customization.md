---
title: "Customization"
component: "DateRangePicker"
description: "Date range picker gives complete control to the user to customize overall appearance of the date range picker in their application."
---

# Customization

DateRangePicker makes available for the UI customization which can be achieved with events, properties that are available with this component.

## Day cell format

[`renderDayCell`](../api/daterangepicker/renderDayCellEventArgs#renderdaycelleventargs) is a
  event which provides the option to customize each day cell while rendering itself.
   The following example disables the weekends of every month using `renderDayCell` event.
 Here we have used the `e-disabled` class to highlight the disabled date.

{% tab template="daterangepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the daterangepicker component
import { DateRangePickerComponent, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    public onRenderDayCell(args: RenderDayCellEventArgs): void {
        if ((args.date as Date).getDay() === 0 || (args.date as Date).getDay() === 6) {
            // sets isDisabled to true to disable the date.
            args.isDisabled = true;
        }
    }

    public render() {
        return <DateRangePickerComponent renderDayCell={this.onRenderDayCell} placeholder='Select a range' />
    }
};

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## First day of week

Start day in a week will differ based on culture. But, you can customize this based on application needs also.
For this, you can make use of `firstDayOfWeek` property.
By default, first day of week in en-US is a Sunday.

In following sample, it customized to Monday with help of this property.

{% tab template="daterangepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the daterangepicker component
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    private startDay:number = 1;

    public render() {
        return <DateRangePickerComponent firstDayOfWeek={this.startDay} placeholder='Select a range' />
    }
};

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Preset ranges

DateRangePicker provides an option to set the predefined ranges in a DateRangePicker
via [`presets`](../api/daterangepicker#presets) properties with the corresponding label.
This property will accept the values in the order of label, start date (date object),
end date (date object) and append these ranges in a component for quick selection.

In following sample, you can choose the frequently using ranges options from the list of ranges itself easily.

{% tab template="daterangepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the daterangepicker component
import { DateRangePickerComponent, PresetsModel } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    private presets: PresetsModel[] = [
        { label: 'Today', start: new Date(), end: new Date() },
        { label: 'Last Week', start: new Date(new Date().setDate(new Date().getDate() - 7)), end: new Date() }
        ];

    public render() {
        return <DateRangePickerComponent placeholder='Select a range' presets={this.presets} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [How to customize DateRangePicker using cssClass](./how-to/customization-using-cssclass)
* [How to disable DateRangePicker component](./how-to/disable-the-daterangepicker-component)
* [How to customize the DateRangePicker day header](./how-to/customize-the-daterangepicker-day-header)