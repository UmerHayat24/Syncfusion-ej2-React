---
title: "React Toast Configuring Options"
component: "Toast"
description: "The Toast control configuration section explains how to customize the appearance of the Toast control using built-in APIs."
---

# Configuring options

This section explains on customizing the Toast appearance using built-in APIs.

## Title and content template

Toast can be created with the notification message. The message contains [`title`](../../api/toast#title) and [`content`](../../api/toast#content) of the Toasts. Title and contents are adaptable in any resolution.

> Title or Content property can be given as HTML element/element ID as a string that can be displayed as a Toast.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent } from '@syncfusion/ej2-react-notifications';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public position = { X: 'Center' };

  public toastCreated(): void {
    this.toastInstance.show();
  }

  public toastShow() {
    this.toastInstance.show();
  }

  public render() {
    return (
      <div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent ref={toast => this.toastInstance = toast!} title="Matt sent you a friend request" content="Hey, wanna dress up as wizards and ride our hoverboards?" position={this.position} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
}
export default App;
```

{% endtab %}

## Specifying custom target

By default toast can be rendered in the document body, we can change the target position for toast rendering using [`target`](../../api/toast#target) property. Based on the target [`position`](../../api/toast#position) will update.

## Close Button

By default [`showCloseButton`](../../api/toast#showclosebutton) will not enabled. We can enable it by setting true value. Before expiring toast we can use to close or destroy toasts manually.

## Progress bar

By default [`showProgressBar`](../../api/toast#showprogressbar) will not enabled. If we enabled it can visually indicate how long time to get toast expires. Based on the `timeOut` property Progress bar will appear.

### Progress bar direction

By default, the [progressDirection](../../api/toast/#progressDirection) is set to "Rtl" and it will appear from right to left direction. You can change the progressDirection to "Ltr" to make it appear from left to right direction.

## Newest on top

In default, newly created toasts will append next with existing toast. We can change the Sequence like inserting before the toast, by enabling the [`newestOnTop`](../../api/toast#newestontop).

Here below sample demonstrates the combination of `target`, `showCloseButton`, `showProgressBar` and `newestOnTop` properties in toast.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent } from '@syncfusion/ej2-react-notifications';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public position = { X: 'Center' };

  public toastCreated(): void {
    this.toastShow();
  }

  public toastShow() {
    setTimeout(
      () => {
        this.toastInstance.show();
      }, 600);
  }

  public render() {
    return (
      <div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent ref={toast => this.toastInstance = toast!} title="File Downloading" content="<div class='progress'><span style='width: 80%'></span></div>" position={this.position} showCloseButton='true' target="#toast_target" newestOnTop='true' showProgressBar='true' progressDirection='Ltr' created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
}
export default App;
```

{% endtab %}

## Width and height

we can set toast dimensions through [`width`](../../api/toast#width) and [`height`](../../api/toast#height) property. The height and width can be applied for specific set of toasts. So you can create different toasts with custom dimension.

In default toast can be rendered with '300px' width with 'auto' height

   > In mobile device toast default width gets '100%' width of the page.
   > When we sets toast width as '100%' toast will occupies full width and displayed top or bottom based on position `Y` property.

Both width and height property allows setting pixels/numbers/percentage. The number value is considered as pixels.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent, ChangeEventArgs, CheckBoxComponent, RadioButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent } from '@syncfusion/ej2-react-notifications';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public checkboxObj: CheckBoxComponent;

  constructor(props: any) {
    super(props);
    this.state = {
      content: 'Hey, wanna dress up as wizards and ride our hoverboards?',
      position: { X: 'Center', Y: "Bottom" },
      title: 'Matt sent you a friend request',
      width: 300
    }
  }

  public toastCreated(): void {
    this.toastShow(600);
  }

  public toastShow(timeOutDelay: number) {
    setTimeout(
      () => {
        this.toastInstance.show();
      }, timeOutDelay);
  }

  public checkboxChange(e: any): void {
    if (e.event.target.checked) {
      this.setState({ position: { Y: "Top" } });
      this.toastInstance.hide('All');
      this.toastShow(700);
    }
  }

  public checkboxChange1(e: any): void {
    if (e.event.target.checked) {
      this.setState({ position: { Y: "Bottom" } });
      this.toastInstance.hide('All');
      this.toastShow(700);
    }
  }

  public onChange(e: ChangeEventArgs): void {
    if (e.checked) {
      this.toastInstance.hide('All');
      this.setState({
        content: "<div class='e-custom'>Take a look at our next generation <b>Javascript</b> <a href='https://ej2.syncfusion.com/home/index.html' target='_blank'>LEARN MORE</a></div>",
        width: '100%',
        title: ''
      });
      this.toastShow(500);
    } else {
      this.toastInstance.hide('All');
      this.setState({
        content: 'Hey, wanna dress up as wizards and ride our hoverboards?',
        width: 300,
        title: 'Matt sent you a friend request'
      });
      this.toastShow(500);
    }
  }

  public render() {
    return (
      <div id="container">
        <div id="toast_full_width" className='row'>
          <table>
            <tr>
              <td>
                <div>
                  <RadioButtonComponent checked={true} label='Top' name="toast" change={this.checkboxChange = this.checkboxChange.bind(this)} />
                </div>
              </td>
              <td>
                <div>
                  <RadioButtonComponent checked={true} label='Bottom' name="toast" change={this.checkboxChange1 = this.checkboxChange1.bind(this)} />
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <div>
                  <CheckBoxComponent label='100% Width' ref={scope => this.checkboxObj = scope!} change={this.onChange = this.onChange.bind(this)} />
                </div>
              </td>
            </tr>
          </table>
        </div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this, 500)}> Show Toast </ButtonComponent>
        <ToastComponent ref={toast => this.toastInstance = toast!} width={this.state.width} title={this.state.title} content={this.state.content} position={this.state.position} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
}
export default App;
```

{% endtab %}

## See Also

[Prevent duplicate toasts](./how-to/prevent-duplicate-toast-display/)
[Customize the progress bar](./how-to/customize-progress-bar-theme-and-sizing/)