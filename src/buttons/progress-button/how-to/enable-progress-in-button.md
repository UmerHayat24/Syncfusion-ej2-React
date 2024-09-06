---
title: "Change the text content and styles of the ProgressButton during progress"
component: "ProgressButton"
description: "React ProgressButton how to section, enable the progress option in button"
---

# Enable progress in button

You can enable the background filler UI by setting the [`enableProgress`](https://ej2.syncfusion.com/react/documentation/api/progress-button/#enableprogress) property to `true`.

{% tab template="progress-button/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html, styles.css", compileJsx=true %}

```tsx
import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ProgressButton.
class App extends React.Component<{}, {}> {

  public render() {
    return (
    <div>
      <ProgressButtonComponent content='Spin Left' enableProgress= {true}/>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('progress-button'));
```

{% endtab %}