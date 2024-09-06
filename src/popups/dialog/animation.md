---
title: "React Dialog Animation"
component: "Dialog"
description: "Explains how to open or close the modal dialog control with various animation effects, duration, and delay (animation dialog box)."
---

# Animation

The Dialog can be animated during the open and close actions. Also, user can
customize animation's [`delay`](../api/dialog/animationSettings/#delay),
[`duration`](../api/dialog/animationSettings/#duration)
and [`effect`](../api/dialog/animationSettings/#effect) by using [animationSettings](../api/dialog/#animationsettings) property.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
delay</td><td>
The Dialog animation will start with the mentioned delay</td></tr>
<tr>
<td>
duration</td><td>
Specifies the animation duration to complete with one animation cycle</td></tr>
<tr>
<td>
effect</td><td>
Specifies the animation effects of Dialog open and close actions effect.
<br /><br />
List of supported animation effects:
<br />
'Fade' | 'FadeZoom' | 'FlipLeftDown' | 'FlipLeftUp' | 'FlipRightDown' | 'FlipRightUp' | 'FlipXDown' |
'FlipXUp' | 'FlipYLeft' | 'FlipYRight' | 'SlideBottom' | 'SlideLeft' | 'SlideRight' | 'SlideTop' |
'Zoom'| 'None'
<br /><br />
If the user sets ‘Fade’ effect, then the Dialog will open with ‘FadeIn’ effect and close with ‘FadeOut’ effect
</td></tr>
</table>

In the below sample, `Zoom` effect is enabled. So, The Dialog will open with `ZoomIn`
and close with `ZoomOut` effects.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component {
  public dialogInstance: DialogComponent;

public settings: any = { effect: 'Zoom', duration: 400, delay: 0 };

public buttons: any = [{
    buttonModel: {
        content: 'OK',
        cssClass: 'e-flat',
        isPrimary: true,
    },
    'click': () => {
        this.dialogInstance.hide();
    }
},
{
    buttonModel: {
        content: 'Cancel',
        cssClass: 'e-flat'
    },
    'click': () => {
        this.dialogInstance.hide();
    }
}];

public handleClick() {
    this.dialogInstance.show();
}

public render() {
  return (
  <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
      <DialogComponent width='250px' animationSettings={this.settings} target='#dialog-target' header='Dialog' showCloseIcon={true}  buttons={this.buttons} ref={dialog => this.dialogInstance = dialog!}>
      Dialog enabled with Zoom effect</DialogComponent>
  </div>);
}
}
export default App;
```

{% endtab %}
