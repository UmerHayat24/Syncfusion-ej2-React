# Header Customization

The header part of Scheduler can be customized easily with the built-in options available.

## Show or Hide header bar

By default, the header bar holds the date and view navigation options, through which the user can switch between the dates and various views. This header bar can be hidden from the UI by setting `false` to the `showHeaderBar` property. It's default value is `true`.

{% tab template="schedule/timescale", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
ScheduleComponent, Day, Week, WorkWeek, Inject,  ViewsDirective, ViewDirective } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}  showHeaderBar={false} eventSettings={{ dataSource: this.data }} >
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Customizing header bar

Apart from the default date navigation and view options available on the header bar, you can add custom items into the Scheduler header bar by making use of the `actionBegin` event. Here, an employee image is added to the header bar, clicking on which will open the popup showing that person's short profile information.

{% tab template="schedule/header-bar", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Month, Inject, ActionEventArgs, ToolbarActionArgs
} from '@syncfusion/ej2-react-schedule';
import { createElement, compile, extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import { Popup } from '@syncfusion/ej2-popups';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private profilePopup: Popup;
    private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let userIconItem: ItemModel = {
        align: 'Right', prefixIcon: 'user-icon', text: 'Nancy', cssClass: 'e-schedule-user-icon'
      };
      args.items.push(userIconItem);
    }
  }
   private onActionComplete(args: ActionEventArgs): void {
    let scheduleElement: HTMLInputElement = document.getElementById('schedule') as HTMLInputElement;
    if (args.requestType === 'toolBarItemRendered') {
      let userIconEle: HTMLElement = scheduleElement.querySelector('.e-schedule-user-icon') as HTMLElement;
      userIconEle.onclick = () => {
        this.profilePopup.relateTo = userIconEle;
        this.profilePopup.dataBind();
        if (this.profilePopup.element.classList.contains('e-popup-close')) {
          this.profilePopup.show();
        } else {
          this.profilePopup.hide();
        }
      };
    }
    let userContentEle: HTMLElement = createElement('div', {
      className: 'e-profile-wrapper'
    });
    scheduleElement.parentElement.appendChild(userContentEle);

    let userIconEle: HTMLElement = scheduleElement.querySelector('.e-schedule-user-icon') as HTMLElement;
    let getDOMString: (data: object) => HTMLCollection = compile('<div class="profile-container"><div class="profile-image">' +
      '</div><div class="content-wrap"><div class="name">Nancy</div>' +
      '<div class="destination">Product Manager</div><div class="status">' +
      '<div class="status-icon"></div>Online</div></div></div>');
    let output: HTMLCollection = getDOMString({});
    this.profilePopup = new Popup(userContentEle, {
      content: output[0] as HTMLElement,
      relateTo: userIconEle,
      position: { X: 'left', Y: 'bottom' },
      collision: { X: 'flip', Y: 'flip' },
      targetType: 'relative',
      viewPortElement: scheduleElement,
      width: 185,
      height: 80
    });
    this.profilePopup.hide();
  }
  render() {
    return <ScheduleComponent cssClass='schedule-header-bar' width='100%' height='550px' id='schedule'
              selectedDate={new Date(2018, 1, 15)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)} actionComplete={this.onActionComplete.bind(this)}>
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

## How to display the view options within the header bar popup

By default, the header bar holds the view navigation options, through which the user can switch between various views. You can move this view options to the header bar popup by setting `true` to the `enableAdaptiveUI` property.

{% tab template="schedule/header-bar", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width='100%' height='500px' selectedDate={new Date(2018, 1, 15)} enableAdaptiveUI={true} eventSettings={ {dataSource:this.data
        } }>
          <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> Refer [here](./resources/#adaptive-ui-in-desktop) to know more about adaptive UI in resources scheduler.

## Date header customization

The Scheduler UI that displays the date text on all views are considered as the date header cells. You can customize the date header cells of Scheduler either using `dateHeaderTemplate` or `renderCell` event.

### Using date header template

The `dateHeaderTemplate` option is used to customize the date header cells of day, week, work-week and timeline views.

{% tab template="schedule/date-header", isDefaultActive=true, iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ScheduleComponent, ViewsDirective, ViewDirective, View, Day, Week, WorkWeek, Month, RenderCellEventArgs, Inject, TimelineViews } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend, Internationalization } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private instance: Internationalization = new Internationalization();
    private getDateHeaderText(value: Date): string {
    return this.instance.formatDate(value, { skeleton: 'Ed' });
    }
  private getWeather(value: Date) {
    switch (value.getDay()) {
      case 0:
        return '<div class="weather-text">25°C</div>';
      case 1:
        return '<div class="weather-text">18°C</div>';
      case 2:
        return '<div class="weather-text">10°C</div>';
      case 3:
        return '<div class="weather-text">16°C</div>';
      case 4:
        return '<div class="weather-text">8°C</div>';
      case 5:
        return '<div class="weather-text">27°C</div>';
      case 6:
        return '<div class="weather-text">17°C</div>';
      default:
        return null;
    }
  }
  private dateHeaderTemplate(props): JSX.Element {
    return (<div><div>{this.getDateHeaderText(props.date)}</div><div className="date-text" dangerouslySetInnerHTML={ { __html: this.getWeather(props.date) } }></div></div>);
  }

  render() {
    return <ScheduleComponent width='100%' height='550px' cssClass='schedule-date-header-template'
    selectedDate={new Date(2018, 1, 15)} eventSettings={{ dataSource: this.data }}
    dateHeaderTemplate={this.dateHeaderTemplate.bind(this)}>
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='TimelineWeek' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek, TimelineViews]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Using renderCell event

In month view, the date header template is not applicable and therefore the same customization can be added beside the date text in month cells by making use of the `renderCell` event.

{% tab template="schedule/date-header", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ScheduleComponent, ViewsDirective, ViewDirective, View, Month, RenderCellEventArgs, Inject } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend, Internationalization } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private getWeather(value: Date) {
    switch (value.getDay()) {
      case 0:
        return '<div class="weather-text">25°C</div>';
      case 1:
        return '<div class="weather-text">18°C</div>';
      case 2:
        return '<div class="weather-text">10°C</div>';
      case 3:
        return '<div class="weather-text">16°C</div>';
      case 4:
        return '<div class="weather-text">8°C</div>';
      case 5:
        return '<div class="weather-text">27°C</div>';
      case 6:
        return '<div class="weather-text">17°C</div>';
      default:
        return null;
    }
  }
  private onRenderCell(args: RenderCellEventArgs): void {
    if (args.elementType === 'monthCells') {
      let ele: Element = document.createElement('div');
      ele.innerHTML = this.getWeather(args.date);
      (args.element).appendChild(ele.firstChild);
    }
  }

  render() {
    return <ScheduleComponent width='100%' height='550px' cssClass='schedule-date-header-template'
    renderCell={this.onRenderCell.bind(this)} selectedDate={new Date(2018, 1, 15)} eventSettings={{ dataSource: this.data }}>
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

## Customizing header indent cells

It is possible to customize the header indent cells using the `headerIndentTemplate` option and change the look and appearance in both the vertical and timeline views. In vertical views, You can customize the header indent cells at the hierarchy level and you can customize the resource header left indent cell in timeline views using the template option.

**Example:** To customize the header left indent cell to display resources text, refer to the below code example.

{% tab template="schedule/header-indent", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { Week, TimelineViews, TimelineMonth, Day, ScheduleComponent, ViewsDirective, ViewDirective, ResourcesDirective,
  ResourceDirective, Inject } from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';

class App extends React.Component<{}, {}>{
    public ownerData: object[] = [
        { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, OwnerColor: '#7499e1' }
    ];

    public headerIndentTemplate() {
      return (
        <div className='e-resource-text'>
          <div className="text">Resources</div></div>
      );
    }

  render() {
    return <ScheduleComponent width='100%' height='550px' currentView='Week' headerIndentTemplate={this.headerIndentTemplate} selectedDate={new Date(2018, 3, 1)} eventSettings={{ dataSource: resourceData }} group={{ resources: ['Owners'] }}>
      <ViewsDirective>
          <ViewDirective option='Day'/>
          <ViewDirective option='Week'/>
          <ViewDirective option='TimelineWeek'/>
          <ViewDirective option='TimelineMonth'/>
      </ViewsDirective>
      <ResourcesDirective>
          <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true} dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
          </ResourceDirective>
      </ResourcesDirective>
      <Inject services={[Day ,Week, TimelineViews, TimelineMonth]}/>
  </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
