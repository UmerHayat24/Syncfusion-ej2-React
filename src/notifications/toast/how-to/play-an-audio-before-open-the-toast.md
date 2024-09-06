---
title: "Play an audio before open the React Toast"
component: "Toast"
description: "This example demonstrates how to play audio in the background while opening the Essential JS 2 Toast control."
---

# Play an audio before displaying the Toast

Here below sample demonstrates to playing audio background while opening Toast. Here we have included audio play codes into beforeOpen event Function.

> If you want to stop the audio after displaying Toast use [`open`](../../api/toast#open) event in Toast. please check the Toast Events [`api's`](../../api/toast#events) for further customization.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public timeOutDelay: number = 600;
  public position = { X: 'Right', Y: 'Bottom' };

  public toastCreated(): void {
    this.toastInstance.show();
  }

  public toastShow() {
    const audio: HTMLAudioElement = new Audio('https://drive.google.com/uc?export=download&id=1M95VOpto1cQ4FQHzNBaLf0WFQglrtWi7');
    audio.play();
    setTimeout(
      () => {
        this.toastInstance.show();
      }, this.timeOutDelay);
  }

  public btnClick(): void {
    this.toastShow()
  }

  public render() {
    return (
      <div>
        <ButtonComponent cssClass="e-primary" onClick={this.btnClick = this.btnClick.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent ref={toast => this.toastInstance = toast!} title='Matt sent you a friend request' content='Hey, wanna dress up as wizards and ride our hoverboards?' position={this.position} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
};
export default App;
```

{% endtab %}
