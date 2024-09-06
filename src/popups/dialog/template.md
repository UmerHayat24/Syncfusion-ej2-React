---
title: "React Dialog Template"
component: "Dialog"
description: "Explains how to customize the dialog's user interface (UI) elements such as header, footer, and content using a template."
---

# Template

In Dialog the template support is provided to header, content and footer sections. So any text or HTML content can be appending in these sections.

## Header

The Dialog header content can be provided through the
[`header`](../api/dialog/#header) property, and it will allow both text and any HTML content as a string.
Also in header, close button is provided as built-in support, and this can be enabled through
the [`showCloseIcon`](../api/dialog/#showcloseicon) property.

## Footer

The Dialog footer can be enabled by adding built-in [`buttons`](../api/dialog/#buttons) or providing any HTML string through the [`footerTemplate`](../api/dialog/#footertemplate).

> The [`buttons`](../api/dialog/#buttons) and [`footerTemplate`](../api/dialog/#footertemplate) properties
can't be used at the same time.

## Content

The Dialog content can be provided through the [`content`](../api/dialog/#content) property, and it accepts both text and HTML string as content.

The below example demonstrates the usage of header, footer and content template in the Dialog.

{% tab template="dialog/template", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {}> {
  public dialogInstance: DialogComponent;
  public buttonInstance: HTMLElement;
  public dialogTextInstance: HTMLSpanElement;

  public handleClick = () => {
      this.dialogInstance.show();
  }

  public header(): JSX.Element {
      return (
      <div>
          <img className="img2" src="https://ej2.syncfusion.com/products/typescript/dialog/template/images/1.png"/>
          <div title="Nancy" className="e-icon-settings dlg-template">Nancy</div>
      </div>
      )
  }

  public footerTemplate(): JSX.Element {
      return (
          <div>
              <input id="inVal" className="e-input" type="text"  placeholder="Enter your message here!"/>

              <button id="sendButton" className="e-control e-btn e-primary" data-ripple="true">Send</button>
          </div>
      )
  }

  public dialogClose = () => {
      this.buttonInstance.style.display='inline-block';
  }

  public dialogOpen = () => {
      this.buttonInstance.style.display='none';
  }

  public keyDown = (e: any) => {
              if (e.keyCode === 13) { this.updateTextValue(); }
  }

  public updateTextValue = () => {
      const enteredVal: HTMLInputElement = document.getElementById('inVal') as HTMLInputElement;
      const dialogTextElement: HTMLElement = document.getElementsByClassName('dialogText')[0] as HTMLElement;
      if ( enteredVal.value !== '') {
          dialogTextElement.innerHTML = enteredVal.value;
      }
      enteredVal.value = '';

  }

  public componentDidMount() {
      setTimeout(() => {
          (document as any).getElementById('sendButton').onkeydown = (e: any) => {
              if (e.keyCode === 13) { this.updateTextValue(); }
          };

          (document as any).getElementById('inVal').onkeydown = (e: any) => {
              if (e.keyCode === 13) { this.updateTextValue(); }
          };

          (document as any).getElementById('sendButton').onclick = (): void => {
              this.updateTextValue();
          };
      });
  }

  public render() {
    return (
    <div className="App" id='dialog-target'>
        <button className='e-control e-btn' id='targetButton1' ref={buttonElement => this.buttonInstance = buttonElement!} role='button' onClick={this.handleClick = this.handleClick}>Open</button>
        <DialogComponent width='350px' target='#dialog-target' header={this.header} footerTemplate={this.footerTemplate } showCloseIcon={true}
         open= {this.dialogOpen} close= {this.dialogClose}
         ref={dialog => this.dialogInstance = dialog!}>
              <div className="dialogContent">
                      <span className="dialogText">Greetings Nancy! When will you share me the source files of the project?</span>
              </div>
        </DialogComponent>
    </div>);
  }
}
export default App;

```

{% endtab %}

## See Also

* [How to add an icon to dialog buttons](./how-to/add-an-icons-to-dialog-buttons)
* [How to customize the dialog appearance](./how-to/customize-the-dialog-appearance)
