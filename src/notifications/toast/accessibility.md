---
title: "React Toast Accessibility"
component: "Toast"
description: "Toast control has accessibility support to access the features via keyboard, screen readers, or other assistive technology devices."
---

# Accessibility

The Toast component has been designed keeping in mind the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications, by applying
 the prompt WAI-ARIA roles, states, and properties along with the keyboard support. Thus, making it usable for people who use assistive WAI-ARIA Accessibility supports that is achieved through the attributes.
It helps to provides information about the elements in a document for assistive technology.
The component implements the keyboard navigation support by following the
  [WAI-ARIA practices](https://www.w3.org/TR/wai-aria-practices/) and tested in major screen readers.

## ARIA attributes

<!-- markdownlint-disable MD033 -->

| Class | Description |
| -------- | -------- |
| role | <b>alert:</b> <br/>   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Identifies the element as the container where alert content will be added or updated. |

{% tab template="toast/toast", sourceFiles="app/App.tsx", isDefaultActive=true, compileJsx=true  %}

```typescript
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";

class App extends React.Component<{}, {}> {
  public toastInstance:ToastComponent;

  public toastCreated(): void {
    this.toastInstance.show();
  }

  public render() {
    return (
      <ToastComponent ref={ toast => this.toastInstance = toast!} title="Sample Toast Title" content="Sample Toast Content" created={this.toastCreated = this.toastCreated.bind(this)} />
    );
  }
};
export default App;
```

{% endtab %}