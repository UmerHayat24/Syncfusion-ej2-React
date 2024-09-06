---
title: "Print"
component: "DocumentEditor"
description: "Learn how to print the document in JavaScript document editor and customize page size, margins, and more during print."
---

# Print

To print the document, use the `print` method from document editor instance.

Refer to the following example for showing a document and print it.

{% tab template="document-editor/print" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, Print } from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(Print);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    onPrint(): void {
        //Print the document content.
        this.documenteditor.print();
    }
    public componentDidMount(): void {
        let sfdt: string = `{
            "sections": [
                {
                    "blocks": [
                        {
                            "inlines": [
                                {
                                    "characterFormat": {
                                        "bold": true,
                                        "italic": true
                                    },
                                    "text": "Hello World"
                                }
                            ]
                        }
                    ],
                    "headersFooters": {
                    }
                }
            ]
        }`;
        setTimeout(() => {
            //Open the document in Document Editor.
            this.documenteditor.open(sfdt);
        });
    }

    render() {
        return (
            <div>
                <button onClick={this.onPrint.bind(this)}>Print</button>
                <DocumentEditorComponent
                    id="container"
                    ref={scope => {
                        this.documenteditor = scope;
                    }}
                    enablePrint={true}
                    height={'330px'}
                />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

Refer to the following example for creating a document and print it.

{% tab template="document-editor/print" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent,
    DocumentEditor,
    Print,
    Editor, Selection, EditorHistory, SfdtExport
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditor.Inject(Print, Editor, Selection, SfdtExport, EditorHistory);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    onPrint(): void {
        //Print the document content.
        this.documenteditor.print();
    }

    render() {
        return (
            <div>
                <button onClick={this.onPrint.bind(this)}>Print</button>
                <DocumentEditorComponent
                    id="container"
                    height={'330px'}
                    ref={scope => {
                        this.documenteditor = scope;
                    }}
                    enablePrint={true} isReadOnly={false} enableSelection={true} enableSfdtExport={true} enableEditor={true} enableEditorHistory={true}
                />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

> DocumentEditor features are segregated into individual feature-wise modules. To use print inject `Print` module using the `DocumentEditor.Inject(Print)`.
> To enable print for a document editor instance, set enablePrint as true.

## Print using window object

You can print the document in document editor by passing the window instance. This is useful to implement print in third party frameworks such as electron, where the window instance will not be available. Refer to the following example.

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent,
    DocumentEditor,
    Print,
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditor.Inject(Print);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        //Print the document content.
        this.documenteditor.print(window);
    }

    render() {
        return (
            <DocumentEditorComponent
                id="container"
                height={'330px'}
                ref={scope => {
                    this.documenteditor = scope;
                }}
                enablePrint={true}
            />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Page setup

Some of the print options cannot be configured using JavaScript. Refer to the following links to learn more about the browser page setup:

* [`Chrome`](https://support.google.com/chrome/answer/1069693?hl=en&visit_id=1-636335333734668335-3165046395&rd=1/)
* [`Firefox`](https://support.mozilla.org/en-US/kb/how-print-web-pages-firefox/)

However, you can customize margins, paper, and layout options by modifying the section format properties using page setup dialog

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, DocumentEditor, Print, Editor, Selection, EditorHistory, PageSetupDialog, SfdtExport } from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditor.Inject(Print, Editor, Selection, EditorHistory, SfdtExport, PageSetupDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        //Open page setup dialog.
        this.documenteditor.showPageSetupDialog();
    }

    render() {
        return (
            <DocumentEditorComponent
                id="container"
                height={'330px'}
                ref={scope => {
                    this.documenteditor = scope;
                }}
                enablePrint={true}
                isReadOnly={false}
                enableSelection={true}
                enableSfdtExport={true}
                enableEditor={true}
                enableEditorHistory={true}
                enablePageSetupDialog={true}
            />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

By customizing margins, papers, and layouts, the layout of the document will be changed in document editor. To modify these options during print operation, serialize the document as SFDT using the `serialize` method in document editor instance and open the SFDT data in another instance of document editor in separate window.

The following example shows how to customize layout options only for printing.

{% tab template="document-editor/print" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, DocumentEditor, Print, Editor, Selection, EditorHistory, SfdtExport, } from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditor.Inject(Print, Editor, Selection, EditorHistory, SfdtExport);
export class Default extends React.Component<{}, {}> {
    public documenteditor1: DocumentEditorComponent;
    public documenteditor2: DocumentEditorComponent;

    onPrint() {
        //Serialize the document content.
        let sfdtData = this.documenteditor1.serialize();
        //Open the serialized content in Document Editor.
        this.documenteditor2.open(sfdtData);
        //Set A5 paper size
        this.documenteditor2.selection.sectionFormat.pageWidth = 419.55;
        this.documenteditor2.selection.sectionFormat.pageHeight = 595.3;
        //Print the document content.
        this.documenteditor2.print();
    }
    render() {
        return (
            <div>
                <button onClick={this.onPrint.bind(this)}>Print</button>
                <DocumentEditorComponent
                    id="DocumentEditor"
                    height={'330px'}
                    ref={scope => {
                        this.documenteditor1 = scope;
                    }}
                    enablePrint={true}
                    isReadOnly={false}
                    enableSelection={true}
                    enableSfdtExport={true}
                    enableEditor={true}
                    enableEditorHistory={true}
                />
                <DocumentEditorComponent
                    id="DocumentEditor2"
                    height={'330px'}
                    ref={scope => {
                        this.documenteditor2 = scope;
                    }}
                    enablePrint={true}
                    isReadOnly={false}
                    enableSelection={true}
                    enableSfdtExport={true}
                    enableEditor={true}
                    enableEditorHistory={true}
                />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [Feature modules](../document-editor/feature-module)
* [Page Setup dialog](../document-editor/dialog#page-setup-dialog)