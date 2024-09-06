# Context Menu

You can display context menu on work cells and appointments of Scheduler by making use of the `ContextMenu` control manually from the application end. In the following code example, context menu control is being added from sample end and set its target as `Scheduler`.

On Scheduler cells, you can display the menu items such as `New Event`, `New Recurring Event` and `Today` option. For appointments, you can display its related options such as `Edit Event` and `Delete Event`. The default event window can be opened for appointment creation and editing using the `openEditor` method of Scheduler.

The deletion of appointments can be done by using the `deleteEvent` public method. Also, the `selectedDate` property can be used to navigate between different dates.

> You can also display custom menu options on Scheduler cells and appointments. Context menu will open on tap-hold in responsive mode.

{% tab template="schedule/context-menu", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend, closest, isNullOrUndefined, remove, removeClass } from '@syncfusion/ej2-base';
import { Query, DataManager } from '@syncfusion/ej2-data';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, CellClickEventArgs,
  Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { BeforeOpenCloseMenuEventArgs, MenuEventArgs, MenuItemModel, ContextMenuComponent } from '@syncfusion/ej2-react-navigations';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private menuObj: ContextMenuComponent;
  private eventObj: { [key: string]: Object };
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private selectedTarget: Element;
  private menuItems: MenuItemModel[] = [
    {
      text: 'New Event',
      iconCss: 'e-icons new',
      id: 'Add'
    }, {
      text: 'New Recurring Event',
      iconCss: 'e-icons recurrence',
      id: 'AddRecurrence'
    }, {
      text: 'Today',
      iconCss: 'e-icons today',
      id: 'Today'
    }, {
      text: 'Edit Event',
      iconCss: 'e-icons edit',
      id: 'Save'
    }, {
      text: 'Edit Event',
      id: 'EditRecurrenceEvent',
      iconCss: 'e-icons edit',
      items: [{
        text: 'Edit Occurrence',
        id: 'EditOccurrence'
      }, {
        text: 'Edit Series',
        id: 'EditSeries'
      }]
    }, {
      text: 'Delete Event',
      iconCss: 'e-icons delete',
      id: 'Delete'
    }, {
      text: 'Delete Event',
      id: 'DeleteRecurrenceEvent',
      iconCss: 'e-icons delete',
      items: [{
        text: 'Delete Occurrence',
        id: 'DeleteOccurrence'
      }, {
        text: 'Delete Series',
        id: 'DeleteSeries'
      }]
    }
  ];

  private onMenuItemSelect(args: MenuEventArgs): void {
    let selectedMenuItem: string = args.item.id;
    if (this.selectedTarget.classList.contains('e-appointment')) {
      this.eventObj = this.scheduleObj.getEventDetails(this.selectedTarget) as { [key: string]: Object };
    }
    switch (selectedMenuItem) {
      case 'Today':
        this.scheduleObj.selectedDate = new Date();
        break;
      case 'Add':
      case 'AddRecurrence':
        let selectedCells: Element[] = this.scheduleObj.getSelectedElements();
        let activeCellsData: CellClickEventArgs =
          this.scheduleObj.getCellDetails(selectedCells.length > 0 ? selectedCells : this.selectedTarget);
        if (selectedMenuItem === 'Add') {
          this.scheduleObj.openEditor(activeCellsData, 'Add');
        } else {
          this.scheduleObj.openEditor(activeCellsData, 'Add', null, 1);
        }
        break;
      case 'Save':
      case 'EditOccurrence':
      case 'EditSeries':
        if (selectedMenuItem === 'EditSeries') {
          this.eventObj = new DataManager(this.scheduleObj.eventsData).executeLocal(new Query().where(this.scheduleObj.eventFields.id,
            'equal', this.eventObj[this.scheduleObj.eventFields.recurrenceID] as string | number))[0] as { [key: string]: Object };
        }
        this.scheduleObj.openEditor(this.eventObj, selectedMenuItem);
        break;
      case 'Delete':
        this.scheduleObj.deleteEvent(this.eventObj);
        break;
      case 'DeleteOccurrence':
      case 'DeleteSeries':
        this.scheduleObj.deleteEvent(this.eventObj, selectedMenuItem);
        break;
    }
  }

  private onContextMenuBeforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
    let newEventElement: HTMLElement = document.querySelector('.e-new-event') as HTMLElement;
    if (newEventElement) {
      remove(newEventElement);
      removeClass([document.querySelector('.e-selected-cell')], 'e-selected-cell');
    }
    let targetElement: HTMLElement = args.event.target as HTMLElement;
    if (closest(targetElement, '.e-contextmenu')) {
      return;
    }
    this.selectedTarget = closest(targetElement, '.e-appointment,.e-work-cells,' +
      '.e-vertical-view .e-date-header-wrap .e-all-day-cells,.e-vertical-view .e-date-header-wrap .e-header-cells');
    if (isNullOrUndefined(this.selectedTarget)) {
      args.cancel = true;
      return;
    }
    if (this.selectedTarget.classList.contains('e-appointment')) {
      this.eventObj = this.scheduleObj.getEventDetails(this.selectedTarget) as { [key: string]: Object };
      if (this.eventObj.RecurrenceRule) {
        this.menuObj.showItems(['EditRecurrenceEvent', 'DeleteRecurrenceEvent'], true);
        this.menuObj.hideItems(['Add', 'AddRecurrence', 'Today', 'Save', 'Delete'], true);
      } else {
        this.menuObj.showItems(['Save', 'Delete'], true);
        this.menuObj.hideItems(['Add', 'AddRecurrence', 'Today', 'EditRecurrenceEvent', 'DeleteRecurrenceEvent'], true);
      }
      return;
    }
    this.menuObj.hideItems(['Save', 'Delete', 'EditRecurrenceEvent', 'DeleteRecurrenceEvent'], true);
    this.menuObj.showItems(['Add', 'AddRecurrence', 'Today'], true);
  }

  render() {
    return (
      <div className='schedule-control-section'>
        <div className='control-section'>
          <div className='control-wrapper'>
            <ScheduleComponent height='550px' ref={t => this.scheduleObj = t} selectedDate={new Date(2018, 1, 15)} eventSettings={{ dataSource: this.data }}>
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
                <ViewDirective option='Agenda' />
              </ViewsDirective>
              <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
            </ScheduleComponent>
          </div>
        </div>
        <ContextMenuComponent cssClass='schedule-context-menu' ref={menu => this.menuObj = menu} target='.e-schedule' items={this.menuItems} beforeOpen={this.onContextMenuBeforeOpen.bind(this)} select={this.onMenuItemSelect.bind(this)} />
      </div>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
