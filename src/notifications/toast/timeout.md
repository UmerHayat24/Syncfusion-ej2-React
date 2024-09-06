---
title: "React Toast Timeout"
component: "Toast"
description: "This section explains how to set time-out value for the Toast control, which is used to display toast till the time-out reaches without user interaction."
---

# TimeOut in React Toast component

The [`timeOut`](../../api/toast#timeout) property helps to change the default value of toast expire time. By default, the timeOut value will be `5000` milliseconds. Toast will live till the timeOut reaches without user interaction, the timeOut value will be taken in milliseconds. Once the toast reached a given timeOut it will expire automatically.

## Visual representation of timeOut

The toast component's `expire time` can be visually shown using a [Progress Bar](./config#progress-bar). To show progress bar you must set showProgressbar api as true.

## How long the toast displayed in page

The [`extendedTimeOut`](../../api/toast#extendedtimeout) property is used to decide how long the toast to be displayed after the user hovers on it.

> You can destroy toast at any time by clicking on the close button. The close button can be enabled by `showCloseButton` property as true.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public position = { X: "Right", Y: "Bottom" };
  private buttons: object[] = [
    { model: { content: "Ignore" } },
    { model: { content: "reply" } }
  ];

  public toastCreated(): void {
    this.toastShow();
  }

  public toastShow() {
    const value: number = parseInt((document.getElementById('timeOut') as HTMLInputElement).value, 0);
    this.toastInstance.show({ timeOut: value });
  }

  public contentTemplate() {
    return <p><img src='./laura.png'/></p>;
  }

  public render() {
    return (
      <div>
        <div className='e-float-input'>
          <input type='text' className='e-input' id='timeOut' defaultValue={'0'} required={true} />
          <span className='e-float-line' />
          <label className="e-float-text">TimeOut</label>
        </div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent id="elementToastTime" ref={toast => this.toastInstance = toast!} title="Anjolie Stokes" content={this.contentTemplate} position={this.position} width={230} height={250} buttons={this.buttons} showProgressBar={true} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
};
export default App;
```

{% endtab %}

## Static toast

You can prevent auto-hiding of toast by set timeOut value of timeOut property as zero (0).

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public position = { X: "Right", Y: "Bottom" };
  private buttons: object[] = [
    { model: { content: "Ignore" } },
    { model: { content: "reply" } }
  ];

  public toastCreated(): void {
    this.toastShow();
  }

  public toastShow() {
    const value: number = parseInt((document.getElementById('timeOut') as HTMLInputElement).value, 0);
    this.toastInstance.show({ timeOut: value });
  }

  public contentTemplate() {
    return <p><img src='./laura.png'/></p>;
  }

  public render() {
    return (
      <div>
        <div className='e-float-input'>
          <input type='text' className='e-input' id='timeOut' defaultValue={'0'} required={true} />
          <span className='e-float-line' />
          <label className="e-float-text">TimeOut</label>
        </div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent id="elementToastTime" ref={toast => this.toastInstance = toast!} title="Anjolie Stokes" content={this.contentTemplate} position={this.position} width={230} height={250} buttons={this.buttons} showProgressBar={true} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
};
export default App;
```

{% endtab %}

## See Also

* [Hide the toast on click](./how-to/close-the-toast-with-click-tap/)