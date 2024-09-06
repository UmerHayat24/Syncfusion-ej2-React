---
title: "Prevent toast close with mobile swipe"
component: "Toast"
description: "This example demonstrates how to prevent the identical same Essential JS 2 Toast is displayed on a screen."
---

# Prevent toast close with mobile swipe

You can prevent the toast close with mobile swipe action by setting [beforeClose](../../api/toast/#beforeClose) argument cancel value to true while argument type as a swipe. The following code shows how to prevent toast close with mobile swipe.

The following sample demonstrates preventing toast close with mobile swipe element displaying with custom code blocks.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent } from '@syncfusion/ej2-react-notifications';
import * as React from 'react';
class App extends React.Component {
    constructor() {
        super(...arguments);
        this.position = { X: 'Center' };
    }
    onBeforeClose(e: any):void {
        if (e.type === "swipe") {
            e.cancel = true;
        }
    }
    toastCreated() {
        this.toastInstance.show();
    }
    toastShow() {
        this.toastInstance.show();
    }
    render() {
        return (<div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent ref={toast => this.toastInstance = toast} title="Matt sent you a friend request" content="Hey, wanna dress up as wizards and ride our hoverboards?" position={this.position} beforeClose={this.onBeforeClose=this.onBeforeClose.bind(this)} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>);
    }
}
export default App;
```

{% endtab %}