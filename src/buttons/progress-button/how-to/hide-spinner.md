---
title: "Hide spinner"
component: "ProgressButton"
description: "React ProgressButton how to section, change text content and styles, hide spinner, customize progress."
---

# Hide spinner

You can hide spinner in the ProgressButton by setting the `e-hide-spinner` property to [`cssClass`](../../api/progress-button#cssClass).

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {}> {

  public render() {
    return (
      <ProgressButtonComponent content='Progress' enableProgress = {true} cssClass='e-hide-spinner'/>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}