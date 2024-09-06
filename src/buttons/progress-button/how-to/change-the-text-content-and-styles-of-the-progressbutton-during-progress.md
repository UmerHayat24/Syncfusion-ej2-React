---
title: "Change the text content and styles of the ProgressButton during progress"
component: "ProgressButton"
description: "React ProgressButton how to section, change text content and styles, hide spinner, customize progress."
---

# Change the text content and styles of the ProgressButton during progress

You can change the text content and styles of the ProgressButton during progress by changing the text content and the  [`cssClass`](../../api/progress-button#cssClass) property at the [`begin`](../../api/progress-button#begin) and [`end`](../../api/progress-button#end) events.

{% tab template="progress-button/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {content: string, cssClass: string}> {
  constructor(props: any) {
    super(props);
    this.state = { content: 'Upload', cssClass: 'e-hide-spinner' };
  }

  private begin(): void {
      this.setState({ content: 'Uploading...', cssClass: 'e-hide-spinner e-info' });
  }

  private end(): void {
      this.setState({ content: 'Success', cssClass: 'e-hide-spinner e-success' });
      setTimeout(() => {
          this.setState({ content: 'Upload', cssClass: 'e-hide-spinner' });
      }, 500)
  }

  public render() {
    return (
      <ProgressButtonComponent content={this.state.content} enableProgress cssClass={this.state.cssClass} duration={4000} begin={this.begin.bind(this)} end={this.end.bind(this)}/>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}