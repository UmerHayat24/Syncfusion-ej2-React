# Editor Window Customization

Scheduler makes use of popups and dialog to display the required notifications, as well as includes an editor window with event fields for making the appointment creation and editing process easier. You can also easily customize the editor window and the fields present in it, and can also apply validations on those fields.

## Event editor

The editor window usually opens on the Scheduler, when a cell or event is double clicked. When a cell is double clicked, the detailed editor window opens in "Add new" mode, whereas when an event is double clicked, the same is opened in an "Edit" mode.

In mobile devices, you can open the detailed editor window in edit mode by clicking the edit icon on the popup, that opens on single tapping an event. You can also open it in add mode by single tapping a cell, which will display a `+` indication, clicking on it again will open the editor window.

> You can also prevent the editor window from opening, by rendering Scheduler in a `readonly` mode or by doing code customization within the `popupOpen` event.

### How to change the editor window header title and text of footer buttons

You can change the header title and the text of buttons displayed at the footer of the editor window by changing the appropriate localized word collection used in the Scheduler.

{% tab template="schedule/local-data" iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, Month, ViewsDirective, ViewDirective, Inject } from '@syncfusion/ej2-react-schedule';
import { extend, L10n } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

L10n.load({
    'en-US': {
        'schedule': {
            'saveButton': 'Add',
            'cancelButton': 'Close',
            'deleteButton': 'Remove',
            'newEvent': 'Add Event',
        },
    }
});
class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='500px' selectedDate= {new Date(2018, 1, 15) } eventSettings={ {dataSource:this.data } }>
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='Month' />
            </ViewsDirective>
          <Inject services={[Day, Week, TimelineViews, Month]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### How to change the label text of default editor fields

To change the default labels such as Subject, Location and other field names in the editor window, make use of the `title` property available within the field option of `eventSettings`.

{% tab template="schedule/local-data" iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, Month, ViewsDirective, ViewDirective, Inject } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='500px' selectedDate= {new Date(2018, 1, 15) } eventSettings={ {dataSource:this.data,
        fields: {
            id: 'Id',
            subject: { name: 'Subject', title: 'Event Name' },
            location: { name: 'Location', title: 'Event Location'},
            description: { name: 'Description', title: 'Event Description' },
            startTime: { name: 'StartTime', title: 'Start Duration' },
            endTime: { name: 'EndTime', title: 'End Duration'  }
        }
        } }>
            <ViewsDirective>
                <ViewDirective option='TimelineDay' />
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
            </ViewsDirective>
          <Inject services={[Day, Week, TimelineViews, Month]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Field validation

It is possible to validate the required fields of the editor window from client-side before submitting it, by adding appropriate validation rules to each field. The appointment fields have been extended to accept both `string` and `object` type values. To perform validations, it is necessary to specify object values for the event fields.

{% tab template="schedule/local-data" iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private minValidation: (args: { [key: string]: string }) => boolean = (args: { [key: string]: string }) => {
        return args['value'].length >= 5;
    };
    render() {
    return <ScheduleComponent  width= '100%' height='500px' selectedDate= {new Date(2018, 1, 15) } eventSettings={ {dataSource:this.data,
        fields: {
            id: 'Id',
            subject: { name: 'Subject', validation: { required: true } },
            location: { name: 'Location', validation: { required: true } },
            description: {
                name: 'Description', validation: {
                    required: true, minLength: [this.minValidation, 'Need atleast 5 letters to be entered']
                }
            },
            startTime: { name: 'StartTime', validation: { required: true } },
            endTime: { name: 'EndTime', validation: { required: true } }
        }
        } }>
          <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> Applicable validation rules can be referred from [form validation](http://ej2.syncfusion.com/documentation/form-validator/#validation-rules) documentation.

### Add additional fields to the default editor

The additional fields can be added to the default event editor by making use of the `popupOpen` event which gets triggered before the event editor opens on the Scheduler. The `popupOpen` is a client-side event that triggers before any of the generic popups opens on the Scheduler. The additional field (any of the form elements) should be added with a common class name `e-field`, so as to handle and process those additional data along with the default event object. In the following example, an additional field `Event Type` has been added to the default event editor and its value is processed accordingly.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, PopupOpenEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend, createElement } from '@syncfusion/ej2-base';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'Editor') {
     if (!args.element.querySelector('.custom-field-row')) {
        let row: HTMLElement = createElement('div', { className: 'custom-field-row' });
        let formElement: HTMLElement = args.element.querySelector('.e-schedule-form');
        formElement.firstChild.insertBefore(row, formElement.firstChild.firstChild);
        let container: HTMLElement = createElement('div', { className: 'custom-field-container' });
        let inputEle: HTMLInputElement = createElement('input', {
          className: 'e-field', attrs: { name: 'EventType' }
        }) as HTMLInputElement;
        container.appendChild(inputEle);
        row.appendChild(container);
        let drowDownList: DropDownList = new DropDownList({
          dataSource: [
            { text: 'Public Event', value: 'public-event' },
            { text: 'Maintenance', value: 'maintenance' },
            { text: 'Commercial Event', value: 'commercial-event' },
            { text: 'Family Event', value: 'family-event' }
          ],
          fields: { text: 'text', value: 'value' },
          value: (args.data as { [key: string]: Object }).EventType as string,
          floatLabelType: 'Always', placeholder: 'Event Type'
        });
        drowDownList.appendTo(inputEle);
        inputEle.setAttribute('name', 'EventType');
      }
    }
  }
  
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule}
    eventSettings={ { dataSource: this.data } } popupOpen={this.onPopupOpen.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Customizing the default time duration in editor window

In default event editor window, start and end time duration are processed based on the `interval` value set within the `timeScale` property. By default, `interval` value is set to 30, and therefore the start/end time duration within the event editor will be in a 30 minutes time difference. You can change this duration value by changing the `duration` option within the `popupOpen` event as shown in the following code example.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, PopupOpenEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'Editor') {
      args.duration = 60;
    }
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule}
    eventSettings={ { dataSource: this.data } } popupOpen={this.onPopupOpen.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to prevent the display of editor and quick popups

It is possible to prevent the display of editor and quick popup windows by passing the value `true` to `cancel` option within the `popupOpen` event.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, PopupOpenEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    args.cancel = true;
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule}
    eventSettings={ { dataSource: this.data } } popupOpen={this.onPopupOpen.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

In case, if you need to prevent only specific popups on Scheduler, then you can check the condition based on the popup type. The types of the popup that can be checked within the `popupOpen` event are as follows.

| Type | Description |
|------|-------------|
| Editor | For Detailed editor window.|
| QuickInfo | For Quick popup which opens on cell click.|
| EditEventInfo |For  Quick popup which opens on event click.|
| ViewEventInfo | For Quick popup which opens on responsive mode.|
| EventContainer | For more event indicator popup.|
| RecurrenceAlert | For edit recurrence event alert popup.|
| DeleteAlert | For delete confirmation popup.|
| ValidationAlert | For validation alert popup.|
| RecurrenceValidationAlert | For recurrence validation alert popup.|

## Customizing event editor using template

The event editor window can be customized by making use of the `editorTemplate` option. Here, the custom window design is built with the required fields using the script template and its type should be of **text/x-template**.

Each field defined within template should contain the **e-field** class, so as to allow the processing of those field values internally. The ID of this customized script template section is assigned to the `editorTemplate` option, so that these customized fields will be replaced onto the default editor window.

As we are using our Syncfusion sub-components within our editor using template in the following example, the custom defined form elements needs to be configured as required Syncfusion components such as **DropDownList** and **DateTimePicker** within the `popupOpen` event. This particular step can be skipped, if the user needs to simply use the usual form elements.

Learn how to customize the event editor window using templates from this video:

`youtube:r24VBNlUmGg`

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, Agenda, PopupOpenEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'Editor') {
      let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
      statusElement.setAttribute('name', 'EventType');
    }
  }
  private editorTemplate(props: Object): JSX.Element {
    return (props !== undefined ? <table className="custom-event-editor" style={ { width: '100%', cellpadding: '5' } }><tbody>
      <tr><td className="e-textlabel">Summary</td><td colSpan={4}>
        <input id="Summary" className="e-field e-input" type="text" name="Subject" style={ { width: '100%' } } />
      </td></tr>
      <tr><td className="e-textlabel">Status</td><td colSpan={4}>
        <DropDownListComponent id="EventType" placeholder='Choose status' data-name="EventType" className="e-field" style={{ width: '100%' }} dataSource={['New', 'Requested', 'Confirmed']} value={(props as any).EventType || null}></DropDownListComponent>
      </td></tr>
      <tr><td className="e-textlabel">From</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="StartTime" data-name="StartTime" value={new Date((props as any).startTime || (props as any).StartTime)} className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">To</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="EndTime" data-name="EndTime" value={new Date((props as any).endTime || (props as any).EndTime)} className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">Reason</td><td colSpan={4}>
        <textarea id="Description" className="e-field e-input" name="Description" rows={3} cols={50} style={ { width: '100%', height: '60px !important', resize: 'vertical' } }></textarea>
      </td></tr></tbody></table>: <div></div>);
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule}
    eventSettings={ { dataSource: this.data } } editorTemplate={this.editorTemplate.bind(this)} showQuickInfo={false}
    popupOpen={this.onPopupOpen.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
                <ViewDirective option='Agenda' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### How to add resource options within editor template

The resource field can be added within editor template with multiselect control for allow multiple resources.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, EventSettingsModel,
  ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend, isNullOrUndefined } from '@syncfusion/ej2-base';
import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import { MultiSelectComponent  } from '@syncfusion/ej2-react-dropdowns';
import { eventData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], eventData, null, true) as Object[];
  private eventSettings: EventSettingsModel = { dataSource: this.data };
  private ownerData: Object[] = [
    { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
    { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' },
    { OwnerText: 'Michael', Id: 3, OwnerColor: '#7499e1' }
  ];
  private fields: object = { text: 'OwnerText', value: 'Id' };
  private editorTemplate(props: Object): JSX.Element {
    return (props !== undefined && Object.keys(props).length > 0 ? <table className="custom-event-editor" style={{ width: '100%', padding: '5' }}><tbody>
      <tr><td className="e-textlabel">Summary</td><td colSpan={4}>
        <input id="Summary" className="e-field e-input" type="text" name="Subject" style={{ width: '100%' }} />
      </td></tr>
      <tr><td className="e-textlabel">Owner</td><td colSpan={4}>
        <MultiSelectComponent className="e-field" placeholder='Choose owner' data-name="OwnerId" dataSource={this.ownerData} fields={this.fields} value={props.OwnerId} />
      </td></tr>
      <tr><td className="e-textlabel">From</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="StartTime" data-name="StartTime" value={new Date((props as any).startTime || (props as any).StartTime)} className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">To</td><td colSpan={4} >
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="EndTime" data-name="EndTime" value={new Date((props as any).endTime || (props as any).EndTime)} className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">Reason</td><td colSpan={4}>
        <textarea id="Description" className="e-field e-input" name="Description" rows={3} cols={50}
          style={{ width: '100%', height: '60px !important', resize: 'vertical' }}></textarea>
      </td></tr></tbody></table> : <div></div>);
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)} ref={schedule => this.scheduleObj = schedule}
      eventSettings={this.eventSettings} editorTemplate={this.editorTemplate.bind(this)} showQuickInfo={false}
      group={{ resources: ['Owners'] }}>
      <ResourcesDirective>
        <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={false} dataSource={this.ownerData} textField='OwnerText' idField='Id' allowGroupEdit={false}
        colorField='OwnerColor'></ResourceDirective>
      </ResourcesDirective>
      <ViewsDirective>
        <ViewDirective option='Day' />
        <ViewDirective option='Week' />
        <ViewDirective option='WorkWeek' />
        <ViewDirective option='Month' />
      </ViewsDirective>
      <Inject services={[Day, Week, WorkWeek, Month]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to add recurrence options within editor template

The following code example shows how to add recurrence options within the editor template by importing `RecurrenceEditor`.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ScheduleComponent, RecurrenceEditorComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, Inject, PopupOpenEventArgs, EventSettingsModel } from '@syncfusion/ej2-react-schedule';
import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private recurrObject: RecurrenceEditorComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private eventSettings: EventSettingsModel = { dataSource: this.data };
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'Editor') {
      (this.scheduleObj.eventWindow as any).recurrenceEditor = this.recurrObject;
    }
  }
  private editorTemplate(props: Object): JSX.Element {
    return (props !== undefined ? <table className="custom-event-editor" style={ { width: '100%' } }>
      <tbody>
      <tr><td className="e-textlabel">Summary</td><td colSpan={4}>
        <input id="Summary" className="e-field e-input" type="text" name="Subject" style={{ width: '100%' }} />
      </td></tr>
      <tr><td className="e-textlabel">Status</td><td colSpan={4}>
        <DropDownListComponent id="EventType" placeholder='Choose status' data-name="Status" className="e-field" style={{ width: '100%' }} dataSource={['New', 'Requested', 'Confirmed']}>
        </DropDownListComponent>
      </td></tr>
      <tr><td className="e-textlabel">From</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="StartTime" data-name="StartTime" value={new Date((props as any).startTime || (props as any).StartTime)} className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">To</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="EndTime" data-name="EndTime" value={new Date((props as any).endTime || (props as any).EndTime)} className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">Recurrence</td><td colSpan={4}>
        <RecurrenceEditorComponent ref={recurrObject => this.recurrObject = recurrObject} id='RecurrenceEditor'></RecurrenceEditorComponent>
      </td></tr>
      <tr><td className="e-textlabel">Reason</td><td colSpan={4}>
        <textarea id="Description" className="e-field e-input" name="Description" rows={3} cols={50} style={{ width: '100%', height: '60px !important', resize: 'vertical' }}></textarea>
      </td></tr></tbody>
      </table> : '');
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule}
    eventSettings= { this.eventSettings } editorTemplate={this.editorTemplate.bind(this)} showQuickInfo={false}
    popupOpen={this.onPopupOpen.bind(this)} >
      <ViewsDirective>
        <ViewDirective option='Day' />
        <ViewDirective option='Week' />
        <ViewDirective option='WorkWeek' />
        <ViewDirective option='Month' />
      </ViewsDirective>
      <Inject services={[Day, Week, WorkWeek, Month]} />
    </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Apply validations on editor template fields

In the following code example, validation has been added to the status field.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month,
  EventRenderedArgs, Inject, Resize, DragAndDrop, PopupOpenEventArgs, EJ2Instance
} from '@syncfusion/ej2-react-schedule';
import { extend, isNullOrUndefined } from '@syncfusion/ej2-base';
import { FormValidator } from '@syncfusion/ej2-inputs';
import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'Editor') {
      let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
      statusElement.setAttribute('name', 'EventType');
      if (!isNullOrUndefined(document.getElementById("EventType_Error"))) {
            document.getElementById("EventType_Error").style.display = "none";
            document.getElementById("EventType_Error").style.left = "351px";
        }
        let formElement: HTMLElement = args.element.querySelector('.e-schedule-form') as HTMLElement;
        let validator: FormValidator = ((formElement as EJ2Instance).ej2_instances[0] as FormValidator);
        validator.addRules('EventType', { required: true });
    }
  }
  private onSelect(args: any): void {
    if (!isNullOrUndefined(document.getElementById("EventType_Error"))) {
        document.getElementById("EventType_Error").style.display = "none";
    }
  }

  private editorTemplate(props: Object): JSX.Element {
     return ((props !== undefined) ? <table className="custom-event-editor" style={{ width: '100%', cellpadding: '5' }}><tbody>
      <tr><td className="e-textlabel">Summary</td><td colSpan={4}>
        <input id="Summary" className="e-field e-input" type="text" name="Subject" style={{ width: '100%' }} />
      </td></tr>
      <tr><td className="e-textlabel">Status</td><td colSpan={4}>
        <DropDownListComponent id="EventType" placeholder='Choose status' data-name='EventType' className="e-field" style={{ width: '100%' }}
          dataSource={['New', 'Requested', 'Confirmed']}>
        </DropDownListComponent>
      </td></tr>
      <tr><td className="e-textlabel">From</td><td colSpan={4}>
        <DateTimePickerComponent id="StartTime" format='dd/MM/yy hh:mm a' data-name="StartTime" value={new Date((props as any).startTime || (props as any).StartTime)}
          className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">To</td><td colSpan={4}>
        <DateTimePickerComponent id="EndTime" format='dd/MM/yy hh:mm a' data-name="EndTime" value={new Date((props as any).endTime || (props as any).EndTime)}
          className="e-field"></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">Reason</td><td colSpan={4}>
        <textarea id="Description" className="e-field e-input" name="Description" rows={3} cols={50}
          style={{ width: '100%', height: '60px !important', resize: 'vertical' }}></textarea>
      </td></tr></tbody></table > : <div></div>);
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule} eventSettings={{ dataSource: this.data }}
              editorTemplate={this.editorTemplate.bind(this)} popupOpen={this.onPopupOpen.bind(this)}
              showQuickInfo={false}>
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### How to save the customized event editor using template

The **e-field** class is not added to each field defined within the template, so you should allow to set those field values externally by using the `popupClose` event.

Note: You can allow to retrieve the data only on the `save` and `delete` option. Data cannot be retrieved on the `close` and `cancel` options in the editor window.

The following code example shows how to save the customized event editor using a template by the `popupClose` event.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Week, WorkWeek, Month, Agenda, PopupOpenEventArgs,PopupCloseEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend, isNullOrUndefined } from '@syncfusion/ej2-base';
import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private startObj: DateTimePickerComponent;
  private endObj: DateTimePickerComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'Editor') {
      let subjectElement: HTMLInputElement = args.element.querySelector('#Summary') as HTMLInputElement;
      if (subjectElement) {
        subjectElement.value = ((args.data as { [key: string]: Object })).Subject as string || "";
      }
      let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
      statusElement.setAttribute('name', 'EventType');
      let descriptionElement: HTMLInputElement = args.element.querySelector('#Description') as HTMLInputElement;
      if (descriptionElement) {
        descriptionElement.value = ((args.data as { [key: string]: Object })).Description as string || "";
      }
    }
  }
  private onPopupClose(args: PopupCloseEventArgs): void {
    if (args.type === 'Editor' && !isNullOrUndefined(args.data as { [key: string]: Object })) {
      let subjectElement: HTMLInputElement = args.element.querySelector('#Summary') as HTMLInputElement;
      if (subjectElement) {
        ((args.data as { [key: string]: Object })).Subject = subjectElement.value;
      }
      let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
      if (statusElement) {
        ((args.data as { [key: string]: Object })).EventType  = statusElement.value;
      }
      ((args.data as { [key: string]: Object })).StartTime = this.startObj.value;
      ((args.data as { [key: string]: Object })).EndTime = this.endObj.value;
      let descriptionElement: HTMLInputElement = args.element.querySelector('#Description') as HTMLInputElement;
      if (descriptionElement) {
        ((args.data as { [key: string]: Object })).Description = descriptionElement.value;
      }
    }
  }
  private editorTemplate(props: Object): JSX.Element {
    return (props !== undefined ? <table className="custom-event-editor" style={ { width: '100%', cellpadding: '5' } }><tbody>
      <tr><td className="e-textlabel">Summary</td><td colSpan={4}>
        <input id="Summary" className="e-input" type="text" value = "" name="Subject" style={ { width: '100%' } } />
      </td></tr>
      <tr><td className="e-textlabel">Status</td><td colSpan={4}>
        <DropDownListComponent id="EventType" placeholder='Choose status' data-name="EventType" style={{ width: '100%' }} dataSource={['New', 'Requested', 'Confirmed']} value={(props as any).EventType || null}></DropDownListComponent>
      </td></tr>
      <tr><td className="e-textlabel">From</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="StartTime" data-name="StartTime" ref={(date) => { this.startObj = date }} value={new Date((props as any).startTime || (props as any).StartTime)}></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">To</td><td colSpan={4}>
        <DateTimePickerComponent format='dd/MM/yy hh:mm a' id="EndTime" data-name="EndTime" ref={(date) => { this.endObj = date }} value={new Date((props as any).endTime ||   (props as any).EndTime)}></DateTimePickerComponent>
      </td></tr>
      <tr><td className="e-textlabel">Reason</td><td colSpan={4}>
        <textarea id="Description" className="e-input" name="Description" rows={3} cols={50} style={ { width: '100%', height: '60px !important', resize: 'vertical' } }></textarea>
      </td></tr></tbody></table>: <div></div>);
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule}
    eventSettings={ { dataSource: this.data } } editorTemplate={this.editorTemplate.bind(this)} showQuickInfo={false}
    popupOpen={this.onPopupOpen.bind(this)} popupClose={this.onPopupClose.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
                <ViewDirective option='Agenda' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
            </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

In case, if you need to prevent only specific popups on Scheduler, then you can check the condition based on the popup type. The types of the popup that can be checked within the `popupClose` event are as follows.

| Type | Description |
|------|-------------|
| Editor | For Detailed editor window.|
| QuickInfo | For Quick popup which opens on cell click.|
| EditEventInfo |For  Quick popup which opens on event click.|
| ViewEventInfo | For Quick popup which opens on responsive mode.|
| EventContainer | For more event indicator popup.|
| RecurrenceAlert | For edit recurrence event alert popup.|
| DeleteAlert | For delete confirmation popup.|
| ValidationAlert | For validation alert popup.|
| RecurrenceValidationAlert | For recurrence validation alert popup.|

## Quick popups

The quick info popups are the ones that gets opened, when a cell or appointment is single clicked on the desktop mode. On single clicking a cell, you can simply provide a subject and save it. Also, while single clicking on an event, a popup will be displayed where you can get the overview of the event information. You can also edit or delete those events through the options available in it.

By default, these popups are displayed over cells and appointments of Scheduler and to disable this action, set `false` to `showQuickInfo` property.

> The quick popup that opens while single clicking on the cells are not applicable on mobile devices.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
ScheduleComponent, Day, Week, WorkWeek, TimelineViews, Inject,  ViewsDirective, ViewDirective } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}  showQuickInfo={false} eventSettings={{ dataSource: this.data }} >
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
            </ViewsDirective>
            <Inject services={[Day, TimelineViews, Week, WorkWeek]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to open QuickInfo popup on multiple cell selection

By default the `QuickInfo` popup will open on single click of the cell. To open the quick info popup on multiple cell selection, you need to select the cells and press `enter` key. You can open this popup immediately after multiple cell selection by setting up `true` to `quickInfoOnSelectionEnd` property where as its default value is `false`.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
ScheduleComponent, Day, Week, WorkWeek, TimelineViews, Inject,  ViewsDirective, ViewDirective } from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    render() {
    return <ScheduleComponent width='100%' height='550px' quickInfoOnSelectionEnd={true} >
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
            </ViewsDirective>
            <Inject services={[Day, TimelineViews, Week, WorkWeek]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to change the watermark text of quick popup subject

By default, `Add Title` text is displayed on the subject field of quick popup. To change the default watermark text, change the value of the appropriate localized word collection used in the Scheduler.

```tsx
L10n.load({
    'en-US': {
        'schedule': {
          'addTitle' : 'New Title'
        }
    }
});
```

### Customizing quick popups

The look and feel of the built-in quick popup window, which opens when single clicked on the cells or appointments can be customized by making use of the `quickInfoTemplates` property of the Scheduler. There are 3 sub-options available to customize them easily,

* header - Accepts the template design that customizes the header part of the quick popup.
* content - Accepts the template design that customizes the content part of the quick popup.
* footer - Accepts the template design that customizes the footer part of the quick popup.

{% tab template="schedule/quick-info", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { extend, isNullOrUndefined } from "@syncfusion/ej2-base";
import { ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject, CellClickEventArgs, CurrentAction, Resize, DragAndDrop } from "@syncfusion/ej2-react-schedule";
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private scheduleObj: ScheduleComponent;
  
  public buttonClickActions(e: Event): void {
    let eventData: { [key: string]: Object } = {};
    let actionType: CurrentAction = "Add";
    const action: string = (e.target as HTMLElement).id;

    const getSlotData: Function = (): { [key: string]: Object } => {
      const cellDetails: CellClickEventArgs = this.scheduleObj.getCellDetails(this.scheduleObj.getSelectedElements());
      const eventData: { [key: string]: Object; } = this.scheduleObj.eventWindow.getObjectFromFormData("e-quick-popup-wrapper");
      const addObj: { [key: string]: Object } = {};

      addObj.Id = this.scheduleObj.getEventMaxID();
      addObj.Subject = (eventData.Subject as string).length > 0 ? eventData.Subject : "Add title";
      addObj.StartTime = new Date(+cellDetails.startTime);
      addObj.EndTime = new Date(+cellDetails.endTime);
      addObj.Location = eventData.Location;

      return addObj;
    };

    switch (action) {
      case "add":
        eventData = getSlotData();
        this.scheduleObj.addEvent(eventData);
        break;
      case "edit":
      case "edit-series":
        eventData = this.scheduleObj.activeEventData.event as { [key: string]: Object; };
        actionType = eventData.RecurrenceRule ? action === "edit" ? "EditOccurrence" : "EditSeries" : "Save";

        if (actionType === "EditSeries")
          eventData = this.scheduleObj.eventBase.getParentEvent(eventData, true);

        this.scheduleObj.openEditor(eventData, actionType);
        break;
      case "delete":
      case "delete-series":
        eventData = this.scheduleObj.activeEventData.event as { [key: string]: Object; };
        actionType = eventData.RecurrenceRule ? action === "delete" ? "DeleteOccurrence" : "DeleteSeries" : "Delete";

        if (actionType === "DeleteSeries")
          eventData = this.scheduleObj.eventBase.getParentEvent(eventData, true);

        this.scheduleObj.deleteEvent(eventData, actionType);
        break;
      case "more-details":
        eventData = getSlotData();
        this.scheduleObj.openEditor(eventData, "Add", true);
        break;
      default:
        break;
    }
    this.scheduleObj.closeQuickInfoPopup();
  }

  private header(props: { [key: string]: string }): JSX.Element {
    return (
      <div>
        {props.elementType === "cell" ? (
          <div className="e-cell-header e-popup-header">
            <div className="e-header-icon-wrapper">
              <button id="close" className="e-close e-close-icon e-icons" title="Close" onClick={this.buttonClickActions.bind(this)} />
            </div>
          </div>
        ) : (
            <div className="e-event-header e-popup-header">
              <div className="e-header-icon-wrapper">
                <button id="close" className="e-close e-close-icon e-icons" title="CLOSE" onClick={this.buttonClickActions.bind(this)} />
              </div>
            </div>
          )}
      </div>
    );
  }

  private content(props: { [key: string]: string }): JSX.Element {
    return (
      <div>
        {props.elementType === "cell" ? (
          <div className="e-cell-content e-template">
            <form className="e-schedule-form">
              <div>
                <input className="subject e-field e-input" type="text" name="Subject" placeholder="Title" />
              </div>
              <div>
                <input className="location e-field e-input" type="text" name="Location" placeholder="Location" />
              </div>
            </form>
          </div>
        ) : (
            <div className="e-event-content e-template">
              <div className="e-subject-wrap">
                {props.Subject !== undefined ? (
                  <div className="subject">{props.Subject}</div>
                ) : (
                    ""
                  )}
                {props.Location !== undefined ? (
                  <div className="location">{props.Location}</div>
                ) : (
                    ""
                  )}
                {props.Description !== undefined ? (
                  <div className="description">{props.Description}</div>
                ) : (
                    ""
                  )}
              </div>
            </div>
          )}
      </div>
    );
  }

  private footer(props: { [key: string]: string }): JSX.Element {
    return (
      <div>
        {props.elementType === "cell" ? (
          <div className="e-cell-footer">
            <div className="left-button">
              <button id="more-details" className="e-event-details" title="Extra Details" onClick={this.buttonClickActions.bind(this)}> Extra Details </button>
            </div>
            <div className="right-button">
              <button id="add" className="e-event-create" title="Add" onClick={this.buttonClickActions.bind(this)} > Add </button>
            </div>
          </div>
        ) : (
            <div className="e-event-footer">
              <div className="left-button">
                <button id="edit" className="e-event-edit" title="Edit" onClick={this.buttonClickActions.bind(this)} > Edit </button>
                {!isNullOrUndefined(props.RecurrenceRule) &&
                  props.RecurrenceRule != "" ? (
                    <button id="edit-series" className="e-edit-series" title="Edit Series" onClick={this.buttonClickActions.bind(this)}> Edit Series </button>
                  ) : (
                    ""
                  )}
              </div>
              <div className="right-button">
                <button id="delete" className="e-event-delete" title="Delete" onClick={this.buttonClickActions.bind(this)} > Delete </button>
                {!isNullOrUndefined(props.RecurrenceRule) &&
                  props.RecurrenceRule != "" ? (
                    <button id="delete-series" className="e-delete-series" title="Delete Series" onClick={this.buttonClickActions.bind(this)}> Delete Series </button>
                  ) : (
                    ""
                  )}
              </div>
            </div>
          )}
      </div>
    );
  }
    render() {
    return <ScheduleComponent id="schedule" ref={(schedule: ScheduleComponent) => (this.scheduleObj = schedule)} width="100%" height="550px" selectedDate={new Date(2018, 1, 15)} eventSettings={{ dataSource: this.data }} quickInfoTemplates={{ header: this.header.bind(this), content: this.content.bind(this), footer: this.footer.bind(this) }}>
        <Inject services={[Day, Week, WorkWeek, Month, Agenda, Resize, DragAndDrop]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> The quick popup in adaptive mode can also be customized using `quickInfoTemplates` using `e-device` class.

## More events indicator and popup

When the number of appointments count that lies on a particular time range * default appointment height exceeds the default height of a cell in month view and all other timeline views, a `+ more` text indicator will be displayed at the bottom of those cells. This indicator denotes that the cell contains few more appointments in it and clicking on that will display a popup displaying all the appointments present on that day.

> To disable this option of showing popup with all hidden appointments, while clicking on the text indicator, you can do code customization within the `popupOpen` event.

The same indicator is displayed on all-day row in calendar views such as day, week and work week views alone, when the number of appointment count present in a cell exceeds three. Clicking on the text indicator here will not open a popup, but will allow the expand/collapse option for viewing the remaining appointments present in the all-day row.

The following code example shows how to disable the display of such popups while clicking on the more text indicator.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Month, PopupOpenEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'EventContainer') {
        args.cancel = true;
    }
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule} currentView= 'Month'
    eventSettings={ { dataSource: this.data } } popupOpen={this.onPopupOpen.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to customize the popup that opens on more indicator

The following code example shows you how to customize the default more indicator popup in which number of events rendered count on the day has been shown in the header.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Month, PopupOpenEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend, Internationalization } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === 'EventContainer') {
        let instance: Internationalization = new Internationalization();
        let date: string  = instance.formatDate(args.data.date, { skeleton: 'MMMEd' });
        ((args.element.querySelector('.e-header-date')) as HTMLElement).innerText = date;
        ((args.element.querySelector('.e-header-day')) as HTMLElement).innerText = 'Event count: ' + args.data.event.length;
    }
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule} currentView= 'Month'
    eventSettings={ { dataSource: this.data } } popupOpen={this.onPopupOpen.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[ Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to prevent the display of popup when clicking on the more text indicator

It is possible to prevent the display of popup window by passing the value `true` to `cancel` option within the `MoreEventsClick` event.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Month, MoreEventsClickArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onMoreEventsClick(args: MoreEventsClickArgs): void {
      args.cancel = true;
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule} currentView= 'Month'
    eventSettings={ { dataSource: this.data } } moreEventsClick={this.onMoreEventsClick.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to navigate Day view when clicking on more text indicator

The following code example shows you how to customize the `moreEventsClick` property to navigate to the Day view when clicking on the more text indicator.

{% tab template="schedule/editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Day, Month, MoreEventsClickArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onMoreEventsClick(args: MoreEventsClickArgs): void {
      args.isPopupOpen = false;
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    ref={schedule => this.scheduleObj = schedule} currentView= 'Month'
    eventSettings={ { dataSource: this.data } } moreEventsClick={this.onMoreEventsClick.bind(this)} >
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Month' />
              </ViewsDirective>
              <Inject services={[Day, Month]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
