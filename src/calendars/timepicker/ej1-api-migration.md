---
title: "Migration from Essential JS 1"
component: "TimePicker"
description: "Explains the common steps for migrating from Essential JS 1 application to Essential JS 2 components especially, time picker component."
---

# Migration from Essential JS 1

This article describes the API migration process of TimePicker component from Essential JS 1 to Essential JS 2.

## Time Selection

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
<EJ.TimePicker id="timepicker" value='2:00 AM' ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>Value</i>

```jsx
<TimePickerComponent id="timepicker" value='5/5/2019 2:00 AM'></TimePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Time Format

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
Display time format
</td>
<td>
<b>Property:</b> <i>timeFormat</i>

```jsx
<EJ.TimePicker id="timepicker" timeFormat='hh:mm:ss tt' ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>format</i>

```jsx
<TimePickerComponent id="timepicker" format='HH:mm'></TimePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Time Range

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
Minimum time
</td>
<td>
<b>Property:</b> <i>minTime</i>

```jsx
<EJ.TimePicker id="timepicker" minTime='10:00 AM' ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>min</i>

```jsx
<TimePickerComponent id="timepicker" min='5/5/2019 2:00 AM'></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Maximum time
</td>
<td>
<b>Property:</b> <i>maxTime</i>

```jsx
<EJ.TimePicker id="timepicker" maxTime='10:00 PM' ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>Max</i>

```jsx
<TimePickerComponent id="timepicker" max='5/5/2019 2:00 AM'></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Set current time
</td>
<td>
<b>Method:</b> <i>setCurrentTime()</i>

```jsx
<EJ.TimePicker id="timepicker" create={this.onCreate} ></EJ.TimePicker>

function onCreate() {
    var timeObj = $("#timepicker").data("ejTimePicker");
    timeObj.setCurrentTime();
}
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
private timeValue: Date = new Date();

<TimePickerComponent id="timepicker" value={this.timeValue}></TimePickerComponent>
```

</td>
</tr>
</thead>
</table>

## Disabled Time Ranges

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
Disable time ranges
</td>
<td>
<b>Property:</b> <i>disableTimeRanges</i>

```jsx
var disableTime = [{ startTime: '3:00 AM', endTime: '6:00 AM' }, { startTime: '1:00 PM', endTime: '3:00 PM' }, { startTime: '8:00 PM', endTime: '10:00 PM' }];

<EJ.TimePicker id="timepicker"  disableTimeRanges={disableTime}  ></EJ.TimePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<TimePickerComponent id="timepicker" itemRender={this.itemRanderHandler.bind(this)}></TimePickerComponent>

itemRanderHandler(args) {
    if (args.value.getHours() === 4) {
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
<EJ.TimePicker id="timepicker" cssClass='gradient-lime' ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>cssClass</i>

```jsx
<TimePickerComponent id="timepicker" cssClass="e-custom-style"></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Popup list customization
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>itemRender</i>

```jsx
<TimePickerComponent id="timepicker" itemRender={this.itemRendeHandler.bind(this)}></TimePickerComponent>

itemRanderHandler() {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Show/Hide the popup button
</td>
<td>
<b>Property:</b> <i>showPopupButton</i>

```jsx
<EJ.TimePicker id="timepicker" showPopupButton={false} ></EJ.TimePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<TimePickerComponent id="timepicker" focus={this.onFocus.bind(this)}></TimePickerComponent>

onFocus(args) {
    this.show();
}

.e-control-wrapper .e-input-group-icon.e-time-icon {
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
<EJ.TimePicker id="timepicker" showRoundedCorner={true} ></EJ.TimePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<TimePickerComponent id="timepicker" cssClass="e-custom-style"></TimePickerComponent>

.e-control-wrapper.e-custom-style.e-time-wrapper.e-input-group {
    border-radius: 4px;
}
```

</td>
</tr>
<tr>
<td>
Enable/Disable the animation
</td>
<td>
<b>Property:</b> <i>enableAnimation</i>

```jsx
<EJ.TimePicker id="timepicker" enableAnimation={false} ></EJ.TimePicker>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Interval
</td>
<td>
<b>Property:</b> <i>interval</i>

```jsx
<EJ.TimePicker id="timepicker" interval={120} ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>step</i>

```jsx
<TimePickerComponent id="timepicker" step={120}></TimePickerComponent>
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
<EJ.TimePicker id="timepicker" focusIn={onFocus} ></EJ.TimePicker>

function onFocus() { /** code block */}
```

</td>
<td>
<b>Event:</b> <i>focus</i>

```jsx
<TimePickerComponent id="timepicker" focus={this.onFocus.bind(this)}></TimePickerComponent>

onFocus() {/** code block */ }
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
<EJ.TimePicker id="timepicker" focusOut={onFocusout} ></EJ.TimePicker>

function onFocusout() { }
```

</td>
<td>
<b>Event:</b> <i>blur</i>

```jsx
<TimePickerComponent id="timepicker" blur={this.onBlur.bind(this)}></TimePickerComponent>

onBlur(args) { /** code block */}
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
<TimePickerComponent id="timepicker" created={this.create.bind(this)}></TimePickerComponent>

create(args) {
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
<b>Method:</b> <i>focusOut</i>

```jsx
<TimePickerComponent id="timepicker" created={this.create.bind(this)}></TimePickerComponent>

create(args) {
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
<b>Event:</b> <i>close</i>

```jsx
<TimePickerComponent id="timepicker" close={this.onClose.bind(this)}></TimePickerComponent>

onClose(args) {
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
<b>Event:</b> <i>open</i>

```jsx
<TimePickerComponent id="timepicker" open={this.onOpen.bind(this)}></TimePickerComponent>

onOpen(args) {
    args.cancel = true;
}
```

</td>
</tr>
</thead>
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
<EJ.TimePicker id="timepicker" enableRTL={true} ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>enableRtl</i>

```jsx
<TimePickerComponent id="timepicker" enableRtl={true}></TimePickerComponent>
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
<EJ.TimePicker id="timepicker" enablePersistence={true} ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>enablePersistence</i>

```jsx
<TimePickerComponent id="timepicker" enablePersistence={true}></TimePickerComponent>
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

<EJ.TimePicker id="timepicker" validationRules= {validationRules} ></EJ.TimePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<TimePickerComponent id="timepicker" floatLabelType='Always'> </TimePickerComponent>

var options = { rules: { 'timepicker': { required: true } } };
var formObject = new ej.inputs.FormValidator('#form-element', options);
```

</td>
</tr>
<tr>
<td>
Validation message
</td>
<td>
<b>Property:</b> <i>validationMessages</i>

```jsx
var validationRules = {required: {true}};
var validationMessage = {required: "Required value"};

$.validator.setDefaults({
    errorClass: 'e-validation-error',
    errorPlacement: function (error, element) {
        $(error).insertAfter(element.closest(".e-widget"));
    }
});

<EJ.TimePicker id="timepicker" validationRules= {validationRules} validationMessages= {validationMessage} ></EJ.TimePicker>
```

</td>A
<td>
<b>Can be achieved by</b>

```jsx
<TimePickerComponent id="timepicker" floatLabelType='Always'> </TimePickerComponent>

var options = { rules: {'timepicker': { required: true } },
    customPlacement: (inputElement, errorElement) => { inputElement.parentElement.parentElement.appendChild(errorElement);
}};
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
<EJ.TimePicker id="timepicker" width="300px" ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>width</i>

```jsx
<TimePickerComponent id="timepicker" width="200px"></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Readonly
</td>
<td>
<b>Property:</b> <i>readOnly</i>

```jsx
<EJ.TimePicker id="timepicker" readOnly={true} ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>Readonly</i>

```jsx
<TimePickerComponent id="timepicker" readonly={true}></TimePickerComponent>
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
<TimePickerComponent id="timepicker" showClearButton={true}></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Height
</td>
<td>
<b>Property:</b> <i>Height</i>

```jsx
<EJ.TimePicker id="timepicker" height="50px" ></EJ.TimePicker>
```

</td>
<td>
<b>Can be achieved by</b>

```jsx
<TimePickerComponent id="timepicker" cssClass="e-custom-style"></TimePickerComponent>

.e-control-wrapper.e-custom-style.e-time-wrapper.e-input-group {
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
Watermark text
</td>
<td>
<b>Property:</b> <i>watermarkText</i>

```jsx
<EJ.TimePicker id="timepicker" watermarkText="Enter Time" ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>placeholder</i>

```jsx
<TimePickerComponent id="timepicker" placeholder="Select a Time"></TimePickerComponent>
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
<EJ.TimePicker id="timepicker" enabled={false} ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>enabled</i>

```jsx
<TimePickerComponent id="timepicker" enabled={true}></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Disable the TimePicker
</td>
<td>
<b>Method:</b> <i>disable()</i>

```jsx
<EJ.TimePicker id="timepicker" create={onCreate} ></EJ.TimePicker>

function onCreate(args) {
    var timeObject = $("#time").data("ejTimePicker");
    timeObject.disable();
}
```

</td>
<td>
<b>Property:</b> <i>enabled</i>

```jsx
<TimePickerComponent id="timepicker" enabled={false}></TimePickerComponent>
```

</td>
</tr>
<tr>
<td>
Enable the TimePicker
</td>
<td>
<b>Method:</b> <i>enable()</i>

```jsx
<EJ.TimePicker id="timepicker" create={onCreate} ></EJ.TimePicker>

function onCreate(args) {
    var timeObject = $("#time").data("ejTimePicker");
    timeObject.enable();
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
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>allowEdit</i>

```jsx
<TimePickerComponent id="timepicker" allowEdit={false}></TimePickerComponent>
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
<TimePickerComponent id="timepicker" zIndex="2000"></TimePickerComponent>
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
<TimePickerComponent id="timepicker" floatLabelType="Always"></TimePickerComponent>
```

</td>
</tr>
</thead>
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
<EJ.TimePicker id="timepicker" locale="en-US" ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>locale</i>

```jsx
<TimePickerComponent id="timepicker" locale="en"></TimePickerComponent>
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
<EJ.TimePicker id="timepicker" enableStrictMode={true} ></EJ.TimePicker>
```

</td>
<td>
<b>Property:</b> <i>strictMode</i>

```jsx
<TimePickerComponent id="timepicker" strictMode={true}></TimePickerComponent>
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
<b>Event:</b> <i>close</i>

```jsx
<EJ.TimePicker id="timepicker" close={onClose} ></EJ.TimePicker>

function onClose() {/** code block */ }
```

</td>
<td>
<b>Event:</b> <i>close</i>

```jsx
<TimePickerComponent id="timepicker" close={this.onClose.bind(this)}></TimePickerComponent>

onClose() {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Open
</td>
<td>
<b>Event:</b> <i>open</i>

```jsx
<EJ.TimePicker id="timepicker" open={onOpen} ></EJ.TimePicker>

function onOpen(args) {/** code block */ }
```

</td>
<td>
<b>Event:</b> <i>open</i>

```jsx
<TimePickerComponent id="timepicker" open={this.onOpen.bind(this)}></TimePickerComponent>

onOpen(args) {/** code block */ }
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
<EJ.TimePicker id="timepicker" create={onCreate} ></EJ.TimePicker>

function onCreate(args) {
    var timeObject = $("#time").data("ejTimePicker");
    timeObject.show();
    timeObject.hide();
}
```

</td>
<td>
<b>Method:</b> <i>hide()</i>

```jsx
<TimePickerComponent id="timepicker" created={this.create.bind(this)}></TimePickerComponent>

create() {
    this.show();
    this.hide();
}
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
<EJ.TimePicker id="timepicker" create={onCreate} ></EJ.TimePicker>

function onCreate(args) {
    var timeObject = $("#time").data("ejTimePicker");
    timeObject.show();
}
```

</td>
<td>
<b>Method:</b> <i>show()</i>

```jsx
<TimePickerComponent id="timepicker" cerated={this.onCreate.bind(this)}></TimePickerComponent>

onCreate() {
    this.show();
}
```

</td>
</tr>
</thead>
</table>