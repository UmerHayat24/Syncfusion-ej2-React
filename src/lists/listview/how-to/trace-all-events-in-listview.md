# Trace all events in ListView

The ListView component triggers events based on its actions. The events can be used as extension points to perform
custom operations. Refer to the following steps to trace the ListView events:

1. Render the ListView with
[dataSource](../../api/list-view/#datasource), and
bind the [`actionBegin`](../../api/list-view/#actionbegin),
[`actionComplete`](../../api/list-view/#actioncomplete),
and [`select`](../../api/list-view/#select) events.

2. Perform custom operations in `actionBegin`,`actionComplete`, and select events.

3. Provide event log details for `actionBegin` and `actionComplete` events, and they will be displayed in the event trace panel
when the ListView action starts and the dataSource bound successfully.

4. Get the selected item details from the
[`SelectEventArgs`](../../api/list-view/selectEventArgs/) in the
select event, and display the selected list item text in the event trace panel while selecting list items.

5. Use clear button to remove event trace information.

{% tab template="listview/events", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

interface EventLogState {
  eventData: string[];
}

export default class App extends React.Component<{}, EventLogState> {
  constructor(props: any) {
    super(props);
    this.state = {
      eventData: []
    };
  }

  //Define an array of JSON data
  private data: any[] = [
    { text: "Hennessey Venom", id: "list-01" },
    { text: "Bugatti Chiron", id: "list-02" },
    { text: "Bugatti Veyron Super Sport", id: "list-03" },
    { text: "SSC Ultimate Aero", id: "list-04" },
    { text: "Koenigsegg CCR", id: "list-05" },
    { text: "McLaren F1", id: "list-06" },
    { text: "Aston Martin One- 77", id: "list-07" },
    { text: "Jaguar XJ220", id: "list-08" },
    { text: "McLaren P1", id: "list-09" },
    { text: "Ferrari LaFerrari", id: "list-10" }
  ];

  public btnClick() {
    this.setState({
      eventData: []
    });
  }

  //Handler for actionBegin event trace
  public onActionBegin(): void {
    setTimeout(() => {
      this.setState({
        eventData: [...this.state.eventData, "actionBegin"]
      });
    }, 0);
  }

  //Handler for select event trace
  public onSelect(args: SelectEventArgs): void {
    this.setState({
      eventData: [...this.state.eventData, `${args.text} is selected`]
    });
  }

  //Handler for actionComplete event trace
  public onActionComplete(): void {
    setTimeout(() => {
      this.setState({
        eventData: [...this.state.eventData, "actionComplete"]
      });
    }, 0);
  }

  //Display event log
  public appendElement(html: string): void {
    let span: HTMLElement = document.createElement("span");
    span.innerHTML = html;
    let log: any = document.getElementById("EventLog");
    log.insertBefore(span, log.firstChild);
  }

  render() {
    return (
      <div id="sample">
        <div className="content-wrapper">
          <ListViewComponent
            id="listview-def"
            dataSource={this.data}
            width="250"
            select={this.onSelect.bind(this) as any}
            actionBegin={this.onActionBegin.bind(this) as any}
            actionComplete={this.onActionComplete.bind(this) as any}
          />
        </div>
        <div id="list_event">
          <h4>
            <b>Event Trace</b>
          </h4>
          <div id="evt">
            <div className="eventarea">
              {/*Event log element */}
              <span className="EventLog" id="EventLog">
                <div />
                {this.state.eventData.map((data: string, index: number) => (
                  <div key={index}>{data}</div>
                ))}
              </span>
            </div>
            <div className="evtbtn">
              {/*clear button element */}
              <ButtonComponent id="clear" onClick={this.btnClick.bind(this)}>
                Clear
              </ButtonComponent>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
