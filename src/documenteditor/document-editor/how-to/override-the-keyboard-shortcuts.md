---
title: "How to"
component: "DocumentEditor"
description: "Learn how to work with document editor in real time scenarios like create simple word processor, override keyboard shortcut behaviors, and more."
---

# How to override the keyboard shortcuts in document editor

Document Editor triggers the [`keyDown`](../../api/document-editor/documentEditorKeyDownEventArgs/) event every time when any key is entered and provides an instance of `DocumentEditorKeyDownEventArgs`. You can use the `isHandled` property to override the keyboard shortcut behavior.

## Preventing default keyboard shortcut

The following code shows how to prevent the `CTRL + C` keyboard shortcut for copying selected content in document editor.

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, DocumentEditorKeyDownEventArgs, SfdtExport, Selection, Editor } from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(SfdtExport, Selection, Editor);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        this.documenteditor.keyDown = function (args: DocumentEditorKeyDownEventArgs) {
            let keyCode: number = args.event.which || args.event.keyCode;
            let isCtrlKey: boolean = (args.event.ctrlKey || args.event.metaKey) ? true : ((keyCode === 17) ? true : false);
            //67 is the character code for 'C'
            if (isCtrlKey && keyCode === 67) {
                //To prevent copy operation set isHandled to true
                args.isHandled = true;
            }
        }
    }

    render() {
        return (
            <DocumentEditorComponent
                id="container"
                ref={scope => {
                    this.documenteditor = scope;
                }}
                isReadOnly={false}
                enableSelection={true}
                enableEditor={true}
                height={'330px'}
            />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));
```

{% endtab %}

## Override or define the keyboard shortcut

Override or define a new keyboard shortcut behavior instead of preventing the keyboard shortcut.

For example, `Ctrl + S` keyboard shortcut saves the document in SFDT format by default, and there is no behavior for `Ctrl + Alt + S`. The following code demonstrates how to override the `Ctrl + S` shortcut to save a document in DOCX format and define `Ctrl + Alt + S` to save the document in SFDT format.

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, DocumentEditor, SfdtExport, Selection, Editor, DocumentEditorKeyDownEventArgs } from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(SfdtExport, Selection, Editor);
export class Default extends React.Component<{}, {}> {
    public documentEditor: DocumentEditorComponent;

    public componentDidMount(): void {
        this.documentEditor.keyDown = (args: DocumentEditorKeyDownEventArgs) => {
            let keyCode: number = args.event.which || args.event.keyCode;

            let isCtrlKey: boolean = (args.event.ctrlKey || args.event.metaKey) ? true : ((keyCode === 17) ? true : false);

            let isAltKey: boolean = args.event.altKey ? args.event.altKey : ((keyCode === 18) ? true : false);

            // 83 is the character code for 'S'
            if (isCtrlKey && !isAltKey && keyCode === 83) {
                //To prevent default save operation, set the isHandled property to true
                args.isHandled = true;
                //Download the document in docx format.
                this.documentEditor.save('sample', 'Docx');
                args.event.preventDefault();
            } else if (isCtrlKey && isAltKey && keyCode === 83) {
                //Download the document in sfdt format.
                this.documentEditor.save('sample', 'Sfdt');
            }
        }
    }

    render() {
        return (
            <DocumentEditorComponent
                id="container"
                ref={scope => {
                    this.documentEditor = scope;
                }}
                isReadOnly={false}
                enableSelection={true}
                enableEditor={true}
                height={'330px'}
            />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}