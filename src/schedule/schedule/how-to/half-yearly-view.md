---
title: "Scheduler Year view customization"
component: "Scheduler"
description: "This section explains how to customize the Year view using different properties in scheduler"
---

# Half-yearly view

The year view of our scheduler displays all the 365 days and their related appointments of a particular year. You can customize the year view by using the following properties.

* [`firstMonthOfYear`](../../api/schedule#firstmonthofyear)
* [`monthsCount`](../../api/schedule#monthscount)
* [`monthHeaderTemplate`](../../api/schedule#monthheadertemplate)

In the following code example, you can see how to render only the last six months of a year in the scheduler. To start with the month of  June, `firstMonthYear` is set to 6 and `monthsCount` is set to 6 to render only 6 months.

{% tab template="schedule/year-customizations", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Resize, DragAndDrop, ResourcesDirective, ResourceDirective, Inject, Year as YearView, TimelineYear
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
   private data: Object[] = extend([], resourceData, null, true) as Object[];
  private categoriesData: Object[] = [
    { text: 'Nancy', id: 1, color: '#ffaa00' },
    { text: 'Steven', id: 2, color: '#f8a398' },
    { text: 'Robert', id: 3, color: '#7499e1' },
    { text: 'Smith', id: 4, color: '#5978ee' },
    { text: 'Micheal', id: 5, color: '#df5286' }
  ];
  private getMonthHeaderText(props): JSX.Element {
    return (<div>{props.date.toLocaleString('en-us', { month: 'long' }) + ' ' + props.date.getFullYear()}</div>);
  }
  private resourceHeaderTemplate(props): JSX.Element {
    return (
      <div className="template-wrap">
        <div className="resource-details">
          <div className="resource-name">{props.resourceData.text}</div>
        </div>
      </div>
    );
  }
  render() {
    return <ScheduleComponent
      width="100%"
      height="495px"
      selectedDate={new Date(2021, 7, 15)}
      ref={schedule => (this.scheduleObj = schedule)}
      eventSettings={{ dataSource: this.data }}
      firstMonthOfYear={6}
      monthsCount={6}
      group={{ resources: ['Categories'] }}
      resourceHeaderTemplate={this.resourceHeaderTemplate.bind(this)}
      monthHeaderTemplate={this.getMonthHeaderText.bind(this)}
    >
      <ResourcesDirective>
        <ResourceDirective
          field="TaskId"
          title="Category"
          name="Categories"
          allowMultiple={true}
          dataSource={this.categoriesData}
          textField="text"
          idField="id"
          colorField="color"
        />
      </ResourcesDirective>
      <ViewsDirective>
        <ViewDirective option="Year" />
        <ViewDirective
          option="TimelineYear"
          displayName="Horizontal TimelineYear"
          isSelected={true}
        />
        <ViewDirective
          option="TimelineYear"
          displayName="Vertical TimelineYear"
          orientation="Vertical"
        />
      </ViewsDirective>
      <Inject
        services={[YearView, TimelineYear, Resize, DragAndDrop]}
      />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}