---
title: "React Dialog Getting Started"
component: "Dialog"
description: "Helps to get started with the dialog control along with its key features such as modal dialog, positioning, and draggable."
---

# Getting Started

The following section explains the required steps to build the
Dialog component with its basic usage in step by step procedure.

## Dependencies

The following list of dependencies are required to use the React Dialog component in your application.

```javascript
|-- @syncfusion/ej2-react-popups
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-react-buttons
    |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-base
        |-- @syncfusion/ej2-buttons

```

## Installation and configuration

You can use [Create-react-app](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

<div class='tsx'>

```bash

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [npmjs.com](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install. For this application, we are going to use Dialog component.

To install Dialog component, use the following command

```bash
npm install @syncfusion/ej2-react-popups –save
```

## Adding Dialog to the application

Now, you can start adding React Dialog component to the application. We have added Dialog component in `src/App.tsx`
file using following code.

{% tab compileJsx=true%}

```typescript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {
constructor(props: {}) {
    super(props);
    this.state = {
        hideDialog : false
    };
}
public handleClick() {
    this.setState({ hideDialog: true })
}

public dialogClose = () => {
    this.setState({ hideDialog: false })
}
public render() {
  return (
  <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)} >Open</button>
      <DialogComponent width='250px' content='This is a Dialog with content' target='.App' visible = {this.state.hideDialog} close = {this.dialogClose}/>
  </div>);
}
}
export default App;

```

{% endtab %}

## Adding CSS reference

Import the Dialog component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-popups/styles/material.css";
```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Run the application

Now use the `npm run start` command to run the application in the browser.

```cmd
npm run start
```

The below example shows the Dialog.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true, isDefaultActive=true %}

```javascript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {
  public dialogInstance: DialogComponent;

  constructor(props: {}) {
      super(props);
      this.state = {
          hideDialog : false
      };
  }
  public handleClick() {
      this.setState({ hideDialog: true })
  }
  
  public dialogClose = () => {
      this.setState({ hideDialog: false })
  }
  public render() {
    return (
    <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)} >Open</button>
      <DialogComponent width='250px' content='This is a Dialog with content' target='#dialog-target' visible = {this.state.hideDialog} close = {this.dialogClose}/>
    </div>);
  }
}
export default App;

```

{% endtab %}

> In the dialog control, max-height is calculated based on the dialog target element height. If the target property is not configured, the document.body is considered as a target. Therefore, to show a dialog in proper height, you need to add min-height to the target element.
>If the dialog is rendered based on the body, then the dialog will get the height based on its body element height. If the height of the dialog is larger than the body height, then the dialog's height will not be set. For this scenario, we can set the CSS style for the html and body to get the dialog height.

```css

html, body {
   height: 100%;
}

```

## Modal Dialog

A [modal](../api/dialog/#ismodal) shows an overlay behind the Dialog. So, the user
should interact the Dialog compulsory before interacting with the remaining content in an
application.

While the user clicks the overlay, the action can be handled through the
[`overlayClick`](../api/dialog/#overlayclick) event. In the below sample, the
Dialog close action is performed while clicking on the overlay.

> When the modal dialog is opened, the Dialog's target scrolling will be disabled. The scrolling
will be enabled again once close the Dialog.

{% tab template="dialog/modal", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {
  public dialogInstance: DialogComponent;

    constructor(props: {}) {
        super(props);
        this.state = {
            hideDialog : true
        };
    }

    public onOverlayClick = () => {
        this.setState({ hideDialog: false })
    }

    public dialogClose = () => {
        this.setState({ hideDialog: false })
    }

    public handleClick() {
        this.setState({ hideDialog: true })
    }

    public render() {
      return (
      <div className="App" id='dialog-target'>
          <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)} >Open</button>

        <DialogComponent width='250px' isModal={true} target='#dialog-target' visible = {this.state.hideDialog} close = {this.dialogClose}
           overlayClick={ this.onOverlayClick } >
          This is a modal Dialog </DialogComponent>
      </div>);
    }
}
export default App;
```

{% endtab %}

## Enable header

The Dialog header can be enabled by adding the header content as text or HTML content through the
[`header`](../api/dialog/#header) property.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {}> {
  public render() {
    return (
    <div className="App" id='dialog-target'>
          <DialogComponent width='250px' target='#dialog-target'  showCloseIcon={true} header='Dialog' closeOnEscape = {false}>
          This is a dialog with header </DialogComponent>
      </div>);
  }
}
export default App;
```

{% endtab %}

## Enable footer

The React Dialog provides built-in support to render the `buttons` on the footer (for ex: ‘OK’ or
‘Cancel’ buttons). Each Dialog button allows the user to perform any action while clicking on it.

The primary button will be focused automatically on open the Dialog, and add the [`click`](../api/dialog/buttonPropsModel/#click)
event to handle the actions

> When the Dialog initialize with more than one primary buttons, the first primary button gets focus on open the Dialog.

The below sample render with button and its click event.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {  
  public buttons: any = [{
    buttonModel: {
        content: 'OK',
        cssClass: 'e-flat',
        isPrimary: true,
    },
    'click': () => {
        this.setState({ hideDialog: false })
    }
},
{
    buttonModel: {
        content: 'Cancel',
        cssClass: 'e-flat'
    },
    'click': () => {
        this.setState({ hideDialog: false })
    }
}];

  constructor(props: {}) {
      super(props);
      this.state = {
          hideDialog : true
      };
  }
  
  public handleClick() {
      this.setState({ hideDialog: true })
  }
  
  public dialogClose = () => {
      this.setState({ hideDialog: false })
  }
  
  public render() {
    return (
    <div className="App" id='dialog-target'>
        <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
        <DialogComponent width='250px' target='#dialog-target' close = {this.dialogClose} header='Dialog' visible = {this.state.hideDialog}showCloseIcon={true}  buttons={this.buttons}>
        This is a Dialog with button and primary button </DialogComponent>
    </div>);
  }
}
export default App;

```

{% endtab %}

## Draggable

The Dialog supports to [drag](../api/dialog/#allowdragging) within its target
container by grabbing the Dialog header, which allows the user to reposition the
Dialog dynamically.

> The Dialog can be draggable only when the Dialog header is enabled.
From `16.2.x` version, enabled draggable support for modal dialog also.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {  
  public buttons: any = [{
        buttonModel: {
            content: 'OK',
            cssClass: 'e-flat',
            isPrimary: true,
        },
        'click': () => {
            this.setState({ hideDialog: false })
        }
    },
    {
      buttonModel: {
          content: 'Cancel',
          cssClass: 'e-flat'
      },
      'click': () => {
          this.setState({ hideDialog: false })
      }
    }];

  constructor(props: {}) {
      super(props);
      this.state = {
          hideDialog : true
      };
  }
public handleClick() {
    this.setState({ hideDialog: true })
}

public dialogClose = () => {
    this.setState({ hideDialog: false })
}

public render() {
  return (
  <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
      <DialogComponent width='250px' target='#dialog-target' visible = {this.state.hideDialog} close = {this.dialogClose} header='Dialog' allowDragging={true} showCloseIcon={true}  buttons={this.buttons}>
      This is a Dialog with drag enabled </DialogComponent>
  </div>);
}
}
export default App;

```

{% endtab %}

## Positioning

The Dialog position can be set through the [`position`](../api/dialog/#position) property by
providing X and Y coordinates. The Dialog can be positioned inside the target container based on
the given X and Y values.

For example <!-- markdownlint-disable MD033 --> <code>position:{ X:'center', Y:'center' }</code>
the possible values

* for X is: left, center, right (or) any offset value
* for Y is: top, center, bottom (or) any offset value

The below sample demonstrates the different Dialog positions.

{% tab template="dialog/positioning", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript
import { RadioButtonComponent } from '@syncfusion/ej2-react-buttons';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {  
  public defaultDialogInstance: DialogComponent;
  public PositioningInstance: HTMLElement;

  public position: any;
  constructor(props: {}) {
      super(props);
      this.state = {
          hideDialog : true
      };
      this.position = { X: 'center', Y: 'center' };
  }

  public changePosition = (event:any): void => {
      this.defaultDialogInstance.position = { X: event.currentTarget.value.split(" ")[0], Y: event.currentTarget.value.split(" ")[1] };

      this.PositioningInstance.innerHTML = 'Position: {X: "' + event.currentTarget.value.split(" ")[0] + '", Y: "' + event.currentTarget.value.split(" ")[1] + '"}'
      const txt: string[] = event.target.parentElement.querySelector('.e-label').innerText.split(" ");
      this.PositioningInstance.innerHTML = 'Position: { X: "' + txt[0] + '", Y: "' + txt[1] + '" }';
  }

  public dialogClose = () => {
    this.setState({ hideDialog: false });
  }

  public dialogOpen = () => {
      this.setState({ hideDialog: true });
  }

  public footerTemplate = (): JSX.Element => {
      return (
          <span id="posvalue" />
      )
  }
  public render() {
    return (
      <div className="App" id='dialog-target'>
    <DialogComponent id='defaultDialog' header='Choose a Dialog Position' visible={this.state.hideDialog} showCloseIcon={false} position={this.position} footerTemplate={this.footerTemplate} width='452px' ref={defaultDialog => this.defaultDialogInstance = defaultDialog!}
          target='#dialog-target' open={this.dialogOpen} close={this.dialogClose} closeOnEscape={false}>
          <table id ='poschange'>
          <tbody>
              <tr>
              <td><RadioButtonComponent id='radio1'  label='Left Top' value='left top' name='xy' onClick = {this.changePosition = this.changePosition.bind(this)} /></td>
              <td><RadioButtonComponent id='radio2'  label='Center Top' value='center top' name='xy' onClick={this.changePosition = this.changePosition.bind(this)}/></td>
              <td><RadioButtonComponent id='radio3'  label='Right Top' value='right top' name='xy' onClick={this.changePosition = this.changePosition.bind(this)}/></td>
            </tr>
            <tr>
              <td><RadioButtonComponent id='radio4'  label='Left Center' value='left center' name='xy' onClick={this.changePosition = this.changePosition.bind(this)} /></td>
              <td><RadioButtonComponent id='radio5' checked = {true} label='Center Center' value='center center' name='xy' onClick={this.changePosition = this.changePosition.bind(this)} /></td>
              <td><RadioButtonComponent id='radio6'  label='Right Center' value='right center' name='xy' onClick={this.changePosition = this.changePosition.bind(this)} /></td>
            </tr>
            <tr>
              <td><RadioButtonComponent id='radio7'  label='Left Bottom' value='left bottom' name='xy' onClick={this.changePosition = this.changePosition.bind(this)} /></td>
              <td><RadioButtonComponent id='radio8'  label='Center Bottom' value='center bottom' name='xy' onClick={this.changePosition = this.changePosition.bind(this)} /></td>
              <td><RadioButtonComponent id='radio9'  label='Right Bottom' value='right bottom' name='xy' onClick={this.changePosition = this.changePosition.bind(this)} /></td>
            </tr>
            </tbody>
      </table>
      </DialogComponent>
      </div>
  );
  }
}
export default App;

```

{% endtab %}

## See Also

* [Load dialog content using AJAX](./how-to/load-dialog-content-using-ajax)
* [How to position the dialog on center of the page on scrolling](./how-to/position-the-dialog-on-center-of-the-page-on-scrolling)
* [Prevent closing of modal dialog](./how-to/prevent-closing-of-modal-dialog)
* [Close dialog while click on outside of dialog](./how-to/close-dialog-while-click-on-outside-of-dialog)
* [How to make a reusable alert and confirm dialog](./how-to/render-a-dialog-using-utility-functions)
