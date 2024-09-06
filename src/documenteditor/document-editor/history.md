---
title: "Undo and redo"
component: "DocumentEditor"
description: "Learn how undo and redo can be done in React document editor and how to customize its limit."
---

# History

Document Editor tracks the history of all editing actions done in the document, which allows undo and redo functionality.

## Enable or disable history

Inject the ‘EditorHistory’ module in your application to provide history preservation functionality for ‘DocumentEditor’. Refer to the following code example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor, EditorHistory } from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, EditorHistory);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    public componentDidMount(): void {
        //Enable history module.
        this.documenteditor.enableEditorHistory = true;
    }
    render() {
        return (
            <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

You can enable or disable history preservation for a document editor instance any time using the ‘enableEditorHistory’ property. Refer to the following sample code.

```typescript
editor.enableEditorHistory = false;
```

## Undo and redo

You can perform undo and redo by ‘CTRL+Z’ and ‘CTRL+Y’ keyboard shortcuts. Document Editor exposes API to do it programmatically.
To undo the last editing operation in document editor, refer to the following sample code.

```typescript
editor.editorHistory.undo();
```

To redo the last undone action, refer to the following code example.

```typescript
editor.editorHistory.redo();
```

## Stack size

History of editing actions will be maintained in stack, so that the last item will be reverted first. By default, document editor limits the size of undo and redo stacks to 500 each respectively. However, you can customize this limit. Refer to the following sample code.

```typescript
editor.editorHistory.undoLimit = 400;
editor.editorHistory.redoLimit = 400;
```

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Keyboard shortcuts](../document-editor/keyboard-shortcut/)