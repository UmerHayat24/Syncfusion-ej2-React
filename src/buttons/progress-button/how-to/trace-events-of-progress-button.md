---
title: "Trace events of ProgressButton"
component: "ProgressButton"
description: "React ProgressButton how to section, change text content and styles, hide spinner, customize progress, event trace."
---

# Trace events of ProgressButton

The ProgressButton component triggers events based on its actions. The events can be used as extension points to perform custom operations.

The events available in ProgressButton are [`fail`](../../api/progress-button#fail), [`begin`](../../api/progress-button#begin), [`progress`](../../api/progress-button#progress), and [`end`](../../api/progress-button#end).

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { ProgressButtonComponent, ProgressEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {eventTrace: string}> {
    constructor(props: any) {
        super(props);
        this.state = {
            eventTrace: ''
        }
        this.begin = this.begin.bind(this);
        this.end = this.end.bind(this);
        this.progress = this.progress.bind(this);
        this.fail = this.fail.bind(this);
        this.btnClick = this.btnClick.bind(this);
    }

    public begin(args: ProgressEventArgs): void {
        this.updateEventLog(args);
    }
    public end(args: ProgressEventArgs): void {
        this.updateEventLog(args);
    }
    public progress(args: ProgressEventArgs): void {
        this.updateEventLog(args);
    }
    public fail(args: Event): void {
        this.updateEventLog(args);
    }
    public updateEventLog(args: any): void {
       this.setState({ eventTrace: this.state.eventTrace + args.name + ' Event triggered. <br />' });
    }

    public btnClick(): void {
        this.setState({ eventTrace: '' });
    }

  public render() {
    return (
        <div className='control-section'>
            <div className='progress-btn-section'>
                <ProgressButtonComponent content='Progress' enableProgress = {true} begin={this.begin} end={this.end} progress={this.progress} fail={this.fail}/>
            </div>
            <div className='property-section'>
                <table id='propertyTable' title='Event trace'>
                    <tbody>
                        <th>Event trace:-</th>
                        <tr>
                            <td dangerouslySetInnerHTML={{__html: this.state.eventTrace}}/>
                        </tr>
                    </tbody>
                </table>
            </div>
            <ButtonComponent id='clear' cssClass='e-small' content='Clear' onClick={this.btnClick.bind(this)}/>
        </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}
