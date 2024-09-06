---
title: "Rich text editor How To customize the placeholder style"
component: "Rich Text Editor"
description: "This section for Syncfusion React Rich Text Editor component explains the customization of placeholder style."
---

# How to customize the placeholder style

By using `e-rte-placeholder` class, you can customize the placeholder style.

{% tab template="rich-text-editor/how-to-placeholder", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  private placeholder: string = "Type something";

  public render() {
    return (
      <RichTextEditorComponent placeholder={this.placeholder}>
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}