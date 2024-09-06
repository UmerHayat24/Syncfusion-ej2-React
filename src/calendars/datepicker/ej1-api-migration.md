---
title: "Migration from Essential JS 1"
component: "DatePicker"
description: "Explains the common steps for migrating from Essential JS 1 application to Essential JS 2 components especially, date picker component."
---

# Migration from Essential JS 1

This article describes the API migration process of DatePicker component from Essential JS 1 to Essential JS 2.

## Date Selection

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Setting the value
</td>
<td>
<b>Property:</b> <i>value</i>

```jsx
<EJ.DatePicker id="datepicker" value='5/5/2019' ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>value</i>

```jsx
<DatePickerComponent id="datepicker" value='5/5/2019'></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Date Format

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Display the date format
</td>
<td>
<b>Property:</b> <i>dateFormat</i>

```jsx
<EJ.DatePicker id="datepicker" dateFormat='yyyy/MM/dd' ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>format</i>

```jsx
<DatePickerComponent  id="datepicker" format="yyyy-MM-dd"></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Day header format
</td>
<td>
<b>Property:</b> <i>dayHeaderFormat</i>

```jsx
<EJ.DatePicker id="datepicker" dayHeaderFormat="long" ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
</thead>
</table>

## Calendar Views

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Start view
</td>
<td>
<b>Property:</b> <i>startLevel</i>

```jsx
<EJ.DatePicker id="datepicker" startLevel="year" ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>start</i>

```jsx
<DatePickerComponent id="datepicker" start="Decade"></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Depth view
</td>
<td>
<b>Property:</b> <i>depthLevel</i>

```jsx
<EJ.DatePicker id="datepicker" depthLevel="year" ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>depth</i>

```jsx
<DatePickerComponent id="datepicker" depth="Year"></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Date Range

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Minimum date
</td>
<td>
<b>Property:</b> <i>minDate</i>

```jsx
<EJ.DatePicker id="datepicker" minDate="5/5/2019" ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>min</i>

```jsx
<DatePickerComponent id="datepicker" min="6/6/2019"></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Maximum date
</td>
<td>
<b>Property:</b> <i>maxDate</i>

```jsx
<EJ.DatePicker id="datepicker" maxDate="5/5/2019" ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>max</i>

```jsx
<DatePickerComponent id="datepicker" max="8/8/2017"></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Disabled Dates

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Block-out dates
</td>
<td>
<b>Property:</b> <i>blackoutDates</i>

```jsx
var blackoutDates = [new Date(2016, 4, 10), new Date(2016, 4, 15), new Date(2016, 4, 20), new Date(2016, 4, 22), new Date(2016, 5, 12), new Date(2016, 5, 24)]

<EJ.DatePicker id="timepicker"  blackoutDates={blackoutDates} value="5/5/2016" ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" renderDayCell={this.disableDate.bind(this)}></DatePickerComponent>

disableDate(args) {
    if (args.date.getDay() === 0 || args.date.getDay() === 6) {
        args.isDisabled = true;
        }
    }
```

</td>
</tr>
</thead>
</table>

## Customization

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
CSS Class
</td>
<td>
<b>Property:</b> <i>cssClass</i>

```jsx
<EJ.DatePicker id="datepicker" cssClass="gradient-lime" ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>cssClass</i>

```jsx
<DatePickerComponent id="datepicker" cssClass='gradient-lime'></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Event callback for each cell creation
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>renderDayCell</i>

```jsx
<DatePickerComponent id="datepicker" renderDayCell={this.onRenderCell.bind(this)}></DatePickerComponent>

onRenderCell() {/** code block */}
```

</td>
</tr>
<tr>
<td>
Show/Hide the today button
</td>
<td>
<b>Property:</b> <i>showFooter</i>

```jsx
<EJ.DatePicker id="datepicker" showFooter={false} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>showTodayButton</i>

```jsx
<DatePickerComponent id="datepicker" showTodayButton ={false}></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Show/Hide the other month dates
</td>
<td>
<b>Property:</b> <i>showOtherMonths</i>

```jsx
<EJ.DatePicker id="datepicker" showOtherMonths={false} ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker"></DatePickerComponent>

.e-datepicker .e-calendar .e-content tr.e-month-hide, .e-datepicker .e-calendar .e-content td.e-other-month > .e-day {
        visibility: none;
   }

.e-datepicker .e-calendar .e-content td.e-month-hide, .e-datepicker .e-calendar .e-content td.e-other-month {
        pointer-events: none;
        touch-action: none;
}
```

</td>
</tr>
<tr>
<td>
Show/Hide the disabled date
</td>
<td>
<b>Property:</b> <i>showDisabledRange</i>

```jsx
var blackoutDates = [new Date(2016, 4, 10), new Date(2016, 4, 15), new Date(2016, 4, 20), new Date(2016, 4, 22), new Date(2016, 5, 12), new Date(2016, 5, 24)]

<EJ.DatePicker id="datepicker" showDisabledRange={false} blackoutDates={blackoutDates} ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Show/Hide the popup button
</td>
<td>
<b>Property:</b> <i>showPopupButton</i>

```jsx
<EJ.DatePicker id="datepicker" showPopupButton={false} ></EJ.DatePicker>
```

</td>
<td>
<b>Event:</b> <i>Focus</i>

```jsx
<DatePickerComponent id="datepicker" focus={this.onFocus.bind(this)}></DatePickerComponent>
onFocus(args) {
    this.show();
}

.e-control-wrapper .e-input-group-icon.e-date-icon {
    display: none;
}
```

</td>
</tr>
<tr>
<td>
Enable/Disable the rounded corner
</td>
<td>
<b>Property:</b> <i>showRoundedCorner</i>

```jsx
<EJ.DatePicker id="datepicker" showRoundedCorner={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" cssClass='e-customStyle'></DatePickerComponent>

.e-control-wrapper.e-customStyle.e-date-wrapper.e-input-group {
    border-radius: 4px;
}
```

</td>
</tr>
<tr>
<td>
Skip a month
</td>
<td>
<b>Property:</b> <i>stepMonths</i>

```jsx
<EJ.DatePicker id="datepicker" stepMonths={3} ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" value='5/5/2019' open={this.onOpen.bind(this)}></DatePickerComponent>

onOpen(args){
    datepicker.navigateTo('Year', new Date("03/18/2028"));
}
```

</td>
</tr>
<tr>
<td>
Show/Hide the tooltip
</td>
<td>
<b>Property:</b> <i>showTooltip</i>

```jsx
<EJ.DatePicker id="datepicker" showTooltip={false} ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Today button text
</td>
<td>
<b>Property:</b> <i>buttonText</i>

```jsx
<EJ.DatePicker id="datepicker" buttonText="Now" ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" locale='de'></DatePickerComponent>

L10n.load({
    'de': {
        'datepicker': { placeholder: 'Wählen Sie ein Datum aus',
        `today: 'heute' }
    }
});
```

</td>
</tr>
<tr>
<td>
Display Inline
</td>
<td>
<b>Property:</b> <i>displayInline</i>

```jsx
<EJ.DatePicker id="datepicker" displayInline={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Enable/Disable the animation
</td>
<td>
<b>Property:</b> <i>enableAnimation</i>

```jsx
<EJ.DatePicker id="datepicker" enableAnimation={false} ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Highlight dates
</td>
<td>
<b>Property:</b> <i>highlightSection</i>

```jsx
<EJ.DatePicker id="datepicker"  highlightSection="month" ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker"  renderDayCell={this.highlightDate.bind(this)}></DatePickerComponent>

highlightDate(args) {
    if (args.date.getDate() === 10) {
        args.element.classList.add('e-highlightweekend');
    }
}

.e-highlightweekend {
    background-color: #cfe9f3;
}
```

</td>
</tr>
<tr>
<td>
Highlight weekend
</td>
<td>
<b>Property:</b> <i>highlightWeekend</i>

```jsx
<EJ.DatePicker id="datepicker"  highlightWeekend={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker"  renderDayCell={this.highlightDate.bind(this)}></DatePickerComponent>

highlightDate(args) {
    if (args.date.getDay() === 0 || args.date.getDay() === 6) {
        args.element.classList.add('e-highlightweekend');
    }
}

.e-highlightweekend {
    background-color: #cfe9f3;
}
```

</td>
</tr>
<tr>
<td>
Tooltip format
</td>
<td>
<b>Property:</b> <i>tooltipFormat</i>

```jsx
<EJ.DatePicker id="datepicker"  tooltipFormat="dd/MM/yyyy" ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Special dates
</td>
<td>
<b>Property:</b> <i>specialDates</i>

```jsx
var specialdate = [ { date: new Date(), tooltip: "In Australia" }]

<EJ.DatePicker id="datepicker"  specialDates={specialdate}></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker"  renderDayCell={this.customDates} value='5/5/2017'></DatePickerComponent>

customDates(args) {
    if (args.date.getDate() === 10) {
        var span = document.createElement('span');
        span.setAttribute('class', 'e-icons highlight');
        args.element.firstElementChild.setAttribute('title', 'Birthday !');
        args.element.setAttribute('title', 'Birthday !');
        args.element.setAttribute('data-val', 'Birthday !');
        args.element.appendChild(span);
    }
}
```

</td>
</tr>
<tr>
<td>
FocusIn event
</td>
<td>
<b>Event:</b> <i>focusIn</i>

```jsx
<EJ.DatePicker id="datepicker"  focusIn={onFocus} ></EJ.DatePicker>

function onFocus() {
    /** code block */
}
```

</td>
<td>
<b>Event:</b> <i>focus</i>

```jsx
<DatePickerComponent id="datepicker" focus={this.onFocus.bind(this)}></DatePickerComponent>

onFocus() {
    /** code block */  
}
```

</td>
</tr>
<tr>
<td>
FocusOut event
</td>
<td>
<b>Event:</b> <i>focusOut</i>

```jsx
<EJ.DatePicker id="datepicker"  focusOut={onFocus} ></EJ.DatePicker>

function onFocus()  {
    /** code block */
}
```

</td>
<td>
<b>Event:</b> <i>blur</i>

```jsx
<DatePickerComponent id="datepicker" blur={this.onBlur.bind(this)}></DatePickerComponent>

onBlur()  {
   /** code block */
}
```

</td>
</tr>
<tr>
<td>
FocusIn method
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Method:</b> <i>focusIn()</i>

```jsx
<DatePickerComponent id="datepicker" created={this.create.bind(this)}></DatePickerComponent>

create(args){
    this.focusIn();
}
```

</td>
</tr>
<tr>
<td>
FocusOut method
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Method:</b> <i>focusOut()</i>

```jsx
<DatePickerComponent id="datepicker" created={this.create.bind(this)}></DatePickerComponent>

create(args){
    this.focusIn();
    this.focusOut();
}
```

</td>
</tr>
<tr>
<td>
Prevent popup close
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>Close</i>

```jsx
<DatePickerComponent id="datepicker" close={this.onClose.bind(this)}></DatePickerComponent>

onClose(args) {
    /*Triggers when the popup gets close*/
    args.cancel = true;
}
```

</td>
</tr>
<tr>
<td>
Prevent popup open
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>Open</i>

```jsx
<DatePickerComponent id="datepicker" open={this.onOpen.bind(this)}></DatePickerComponent>

onOpen(args) {
    /*Triggers when the popup gets close*/
    args.cancel = true;
}
```

</td>
</tr>
</table>

## Accessibility

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Enable/Disable the RTL
</td>
<td>
<b>Property:</b> <i>enableRTL</i>

```jsx
<EJ.DatePicker id="datepicker" enableRTL={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>enableRtl</i>

```jsx
<DatePickerComponent id="datepicker" enableRtl={true}></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Persistence

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Enable/Disable the persistence
</td>
<td>
<b>Property:</b> <i>enablePersistence</i>

```jsx
<EJ.DatePicker id="datepicker" enablePersistence={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>enablePersistence</i>

```jsx
<DatePickerComponent id="datepicker" enablePersistence={true}></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Validation

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Validation rules
</td>
<td>
<b>Property:</b> <i>validationRules</i>

```jsx
var validationRules = {required: {true}};

$.validator.setDefaults({
    errorClass: 'e-validation-error',
    errorPlacement: function (error, element) {
        $(error).insertAfter(element.closest(".e-widget"));
        }
});

<EJ.DatePicker id="timepicker" validationRules= {validationRules} ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" floatLabelType='Always'> </DatePickerComponent>

var options = { rules: { 'datepicker': { required: true } } };
var formObject = new ej.inputs.FormValidator('#form-element', options);
```

</td>
</tr>
<tr>
<td>
Validation message
</td>
<td>
<b>Property:</b> <i>validationMessage</i>

```jsx
var validationRules = {required: {true}};
var validationMessage = {required: "Required value"};

$.validator.setDefaults({
    errorClass: 'e-validation-error',
    errorPlacement: function (error, element) {
        $(error).insertAfter(element.closest(".e-widget"));
    }
});

<EJ.DatePicker id="timepicker" validationRules= {validationRules} validationMessage= {validationMessage} ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" floatLabelType='Always'> </DatePickerComponent>

var options = { rules: { 'datepicker': { required: true } },
customPlacement: (inputElement, errorElement) => {
    inputElement.parentElement.parentElement.appendChild(errorElement);
}
var formObject = new ej.inputs.FormValidator('#form-element', options);
```

</td>
</tr>
</thead>
</table>

## Common

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Width
</td>
<td>
<b>Property:</b> <i>width</i>

```jsx
<EJ.DatePicker id="datepicker" width='300px' ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>width</i>

```jsx
<DatePickerComponent id="datepicker" width='300px'></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Readonly
</td>
<td>
<b>Property:</b> <i>readonly</i>

```jsx
<EJ.DatePicker id="datepicker" readOnly={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>readonly</i>

```jsx
<DatePickerComponent id="datepicker" readonly={true}></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Show/Hide the clear button
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>showClearButton</i>

```jsx
<DatePickerComponent id="datepicker" showClearButton={false}></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Height
</td>
<td>
<b>Property:</b> <i>height</i>

```jsx
<EJ.DatePicker id="datepicker" height='50px' ></EJ.DatePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<DatePickerComponent id="datepicker" cssClass='e-custom-style'></DatePickerComponent>

.e-control-wrapper.e-custom-style.e-date-wrapper.e-input-group {
    height: 35px;
}
```

</td>
</tr>
<tr>
<td>
Html Attributes
</td>
<td>
<b>Property:</b> <i>HtmlAttributes</i>

```jsx

var htmlAttributes = {required:"required"}
  
<EJ.TimePicker id="timepicker"  htmlAttributes = {htmlAttributes} ></EJ.TimePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Enable/Disable the week number
</td>
<td>
<b>Property:</b> <i>weekNumber</i>

```jsx
<EJ.DatePicker id="datepicker" weekNumber={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>weekNumber</i>

```jsx
<DatePickerComponent id="datepicker" weekNumber={true}></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Watermark text
</td>
<td>
<b>Property:</b> <i>watermarkText</i>

```jsx
<EJ.DatePicker id="datepicker" watermarkText="enter a date' ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>placeholder</i>

```jsx
<DatePickerComponent id="datepicker" placeholder='Enter date'></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Disable/Enable
</td>
<td>
<b>Property:</b> <i>enabled</i>

```jsx
<EJ.DatePicker id="datepicker" enabled={false}></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>enabled</i>

```jsx
<DatePickerComponent id="datepicker" enabled={false}></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Disable the DatePicker
</td>
<td>
<b>Method:</b> <i>disable()</i>

```jsx
<EJ.DatePicker id="datepicker" create={onCreate}></EJ.DatePicker>

function onCreate(args) {
    var dateObject = $("#datepicker").data("ejDatePicker");
    dateObject.disable();
}
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Enable the DatePicker
</td>
<td>
<b>Method:</b> <i>enable()</i>

```jsx
<EJ.DatePicker id="datepicker" create={onCreate}></EJ.DatePicker>

function onCreate(args) {
    var dateObject = $("#datepicker").data("ejDatePicker");
    dateObject.enable();
}
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Enable/Disable the textBox editing
</td>
<td>
<b>Property:</b> <i>allowEdit</i>

```jsx
<EJ.DatePicker id="datepicker" allowEdit={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>allowEdit</i>

```jsx
<DatePickerComponent id="datepicker" allowEdit={false}></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
zIndex
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>zIndex</i>

```jsx
<DatePickerComponent id="datepicker" zIndex="2000" ></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
Specify the placeholder text behavior
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>floatLabelType</i>

```jsx
<DatePickerComponent id="datepicker" placeholder='Enter date' floatLabelType='Auto'></DatePickerComponent>
```

</td>
</tr>
</table>

## Globalization

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Locale
</td>
<td>
<b>Property:</b> <i>locale</i>

```jsx
<EJ.DatePicker id="datepicker" locale="en-US" ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>locale</i>

```jsx
<DatePickerComponent id="datepicker" locale='en'></DatePickerComponent>
```

</td>
</tr>
<tr>
<td>
First day of week
</td>
<td>
<b>Property:</b> <i>startDay</i>

```jsx
<EJ.DatePicker id="datepicker" startDay={3} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>firstDayOfWeek</i>

```jsx
<DatePickerComponent firstDayOfWeek={5}></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Strict Mode

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Strict mode
</td>
<td>
<b>Property:</b> <i>enableStrictMode</i>

```jsx
<EJ.DatePicker id="datepicker" enableStrictMode={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Property:</b> <i>strictMode</i>

```jsx
<DatePickerComponent id="datepicker" min="5/5/2019" max="6/6/2019" value="7/7/2019" strictMode={true}></DatePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Open and Close

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Close
</td>
<td>
<b>Event:</b> <i>Close</i>

```jsx
<EJ.DatePicker id="datepicker" close={onClose} ></EJ.DatePicker>

function onClose() { /** code block */ }
```

</td>
<td>
<b>Event:</b> <i>Close</i>

```jsx
<DatePickerComponent id="datepicker"  close={this.onClose.bind(this)}></DatePickerComponent>

onClose() { /** code block */ }
```

</td>
</tr>
<tr>
<td>
Hide
</td>
<td>
<b>Method:</b> <i>hide()</i>

```jsx
<EJ.DatePicker id="datepicker" create={onCreate} ></EJ.DatePicker>

function onCreate(args) {
    var dateObject = $("#datepicker").data("ejDatePicker");
    dateObject.show();
    dateObject.hide();
}
```

</td>
<td>
<b>Method:</b> <i>hide()</i>

```jsx
<DateTimePickerComponent id="datetimepicker" created={this.onCreate.bind(this)}></DateTimePickerComponent>

onCreate(args){
    this.show();
    this.hide();
}
```

</td>
</tr>
<tr>
<td>
Open
</td>
<td>
<b>Event:</b> <i>Open</i>

```jsx
<EJ.DatePicker id="datepicker" open={onOpen} ></EJ.DatePicker>

function onOpen() {/** code block */ }
```

</td>
<td>
<b>Event:</b> <i>Open</i>

```jsx
<DatePickerComponent id="datepicker" open={this.onOpen.bind(this)}></DatePickerComponent>

onOpen() {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Show
</td>
<td>
<b>Method:</b> <i>show()</i>

```jsx
<EJ.DatePicker id="datepicker" create={onCreate} ></EJ.DatePicker>

function onCreate(args) {
    var dateObject = $("#datepicker").data("ejDatePicker");
    dateObject.show();
}
```

</td>
<td>
<b>Method:</b> <i>show()</i>

```jsx
<DatePickerComponent id="datepicker" created={this.create.bind(this)} ></DatePickerComponent>

create(args){
    this.show();
}
```

</td>
</tr>
</thead>
</table>

## View Navigation

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Navigate to specific month
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Method:</b> <i>navigateTo()</i>

```jsx
<DatePickerComponent id="datepicker" open={this.onOpen.bind(this)} ></DatePickerComponent>

onOpen(args){
    this.navigateTo('Year', new Date("03/18/2018"));
}
```

</td>
</tr>
<tr>
<td>
Navigation callback
</td>
<td>
<b>Event:</b> <i>Navigate</i>

```jsx
<EJ.DatePicker id="datepicker" navigate={onNavigate} ></EJ.DatePicker>

onNavigate() {/** code block */ }
```

</td>
<td>
<b>Event:</b> <i>Navigated</i>

```jsx
<DatePickerComponent id="datepicker" navigated={this.onNavigated.bind(this)} ></DatePickerComponent>

onNavigated() {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Enable/Disable the drill down
</td>
<td>
<b>Property:</b> <i>allowDirllDown</i>

```jsx
<EJ.DatePicker id="datepicker" allowDirllDown={true} ></EJ.DatePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
</thead>
</table>