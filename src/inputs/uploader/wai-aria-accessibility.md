---
title: "WAI-ARIA Accessibility"
component: "Uploader"
description: "Describes the accessibility standard of the file upload control such as WAI-ARIA attributes, keyboard interaction, theming, etc."
---

# Accessibility

The uploader component characterized with complete ARIA accessibility support that helps to be accessible by
on-screen readers and other assistive technology devices.

## Keyboard interaction

The following are the standard keys that works on uploader component.

| **Keyboard shortcuts** | **Actions** |
| --- | --- |
| <kbd>Tab</kbd> | Move focus to next element. |
| <kbd>Shift + Tab</kbd> | Move focus to previous element. |
| <kbd>Enter</kbd> | Triggers corresponding action to button element. |
| <kbd>Esc</kbd> | Close the file browser dialog alone and cancels the upload on drop the file. |

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
      }
  public render() {
    return (
      <UploaderComponent autoUpload={false} asyncSettings={this.path} />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.