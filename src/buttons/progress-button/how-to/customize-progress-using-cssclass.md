---
title: "Customize progress using cssClass"
component: "ProgressButton"
description: "React ProgressButton how to section, change text content and styles, hide spinner, customize progress."
---

# Customize progress using cssClass

You can customize the background filler UI using the [`cssClass`](../../api/progress-button#cssClass) property.

* Adding `e-vertical` to `cssClass` shows vertical progress.
* Adding `e-progress-top` to `cssClass` shows progress at the top.

You can also show reverse progress by adding custom class to the [`cssClass`](../../api/progress-button#cssClass) property.

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html,progress.css", compileJsx=true %}

```tsx

import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {}> {

  public render() {
    return (<div>
      <ProgressButtonComponent content='Vertical Progress' enableProgress = {true} cssClass='e-hide-spinner e-vertical' duration={4000}/>
      <ProgressButtonComponent content='Progress Top' enableProgress = {true} cssClass='e-hide-spinner e-progress-top' duration={4000}/>
      <ProgressButtonComponent content='Reverse Progress' enableProgress = {true} cssClass='e-hide-spinner e-reverse-progress' duration={4000}/></div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}