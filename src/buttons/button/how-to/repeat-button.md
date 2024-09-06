---
title: "Repeat Button"
component: "Button"
description: "React Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Repeat Button

The Repeat button is a type of Button in that the click event is triggered at regular time interval from the pressed state
till the released state.

The following example explains about how to achieve Repeat Button in mouse and touch events.

{% tab template="button/repeat-button", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple, EventHandler } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from "react";
import * as ReactDOM from "react-dom";

enableRipple(true);

class App extends React.Component<{}, {}> {
    public btn: ButtonComponent;
    private timeout: any = null;
    constructor(props: any) {
        super(props);
        this.mouseDownHandler = this.mouseDownHandler.bind(this);
        this.mouseUpHandler = this.mouseUpHandler.bind(this);
        this.clickEventHandler = this.clickEventHandler.bind(this);
        this.onCreated = this.onCreated.bind(this);
    }
    public onCreated(): void {
        const btnElem = this.btn.element as HTMLElement;
        btnElem.addEventListener("mousedown", this.mouseDownHandler);
        btnElem.addEventListener("mouseup", this.mouseUpHandler);
        btnElem.addEventListener("touchstart", this.mouseDownHandler);
        btnElem.addEventListener("touchend", this.mouseUpHandler);

    }
    public mouseDownHandler(): void {
        this.timeout = setInterval(() => this.processEvents(), 200);
    }
    public onClick(): void {
      (document.getElementById('eventlog') as HTMLElement).innerHTML = '';
    }

    public mouseUpHandler(): void {
        clearInterval(this.timeout);
    }

    public clickEventHandler(): void {
      EventHandler.trigger((document.getElementById('btn') as HTMLElement), "click");
      const span = document.createElement('span');
      span.innerHTML = 'Button click event triggered.<hr>';
      const log: HTMLElement = document.getElementById('eventlog') as HTMLElement;
      log.insertBefore(span, log.firstChild);
    }

    public render() {
        return (
            <div className='container'>
            <div className='btncontainer'>
               <ButtonComponent id='btn' ref={(scope) => { this.btn = scope as ButtonComponent; }} created={this.onCreated} content='Button' onClick = {this.clickEventHandler} />
            </div>
             <div className='event'>
              <table className='table' title ='Event Trace'>
            <tbody>
            <tr>
                <th>Event Trace</th>
            </tr>
            <tr>
                <td>
                    <div className="eventarea">
                        <span id="eventlog" />
                    </div>
                </td>
            </tr>
            <tr>
                <td>
                    <div className="evtbtn">
                        <ButtonComponent id="clr-btn" content='Clear' onClick = {this.onClick} />
                    </div>
                </td>
            </tr>
        </tbody>
        </table>
            </div>
          </div>
        )
    }
    private processEvents(): void {
        const span = document.createElement('span');
        span.innerHTML = 'Button click event triggered.<hr>';
        const log = document.getElementById('eventlog') as HTMLElement;
        log.insertBefore(span, log.firstChild);
    }
}
ReactDOM.render(<App />, document.getElementById('button'));

```

{% endtab %}