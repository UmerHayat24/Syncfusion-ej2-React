---
title: "Hyperlink"
component: "DocumentEditor"
description: "Learn how to insert, delete, or navigate links in React document editor."
---

# Hyperlink

Document Editor supports hyperlink field. You can link a part of the document content to Internet or file location, mail address, or any text within the document.

## Navigate a hyperlink

Document Editor triggers ‘requestNavigate’ event whenever user clicks Ctrl key or tap a hyperlink within the document. This event provides necessary details about link type, navigation URL, and local URL (if any) as arguments, and allows you to easily customize the hyperlink navigation functionality. Refer to the following example.

{% tab template="document-editor/link" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, RequestNavigateEventArgs
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(Selection, SfdtExport);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    // Add event listener for requestNavigate event to customize hyperlink navigation functionality
    requestNavigate = (args: RequestNavigateEventArgs) => {
        if (args.linkType !== 'Bookmark') {
            let link: string = args.navigationLink;
            if (args.localReference.length > 0) {
                link += '#' + args.localReference;
            }
            //Navigate to the specified URL.
            window.open(link);
            args.isHandled = true;
        }
    };

    render() {
        return (
            <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} enableSelection={true} enableSfdtExport={true} requestNavigate={this.requestNavigate.bind(this)} />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

If the selection is in hyperlink, trigger this event by calling ‘navigateHyperlink’ method of ‘Selection’ instance. Refer to the following example.

```typescript
documenteditor.selection.navigateHyperlink();
```

## Copy link

Document Editor copies link text of a hyperlink field to the clipboard if the selection is in hyperlink. Refer to the following example.

```typescript
documenteditor.selection.copyHyperlink();
```

## Add hyperlink

To create a basic hyperlink in the document, press `ENTER` / `SPACEBAR` / `SHIFT + ENTER` / `TAB` key after typing the address, for instance `http://www.google.com`. Document Editor automatically converts this address to a hyperlink field. The text can be considered as a valid URL if it starts with any of the following.

><http://><br>
><https://><br>
>file:///<br>
>www.<br>
>mailto:<br>

Refer to the following example.

{% tab template="document-editor/link" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, RequestNavigateEventArgs
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(Selection, SfdtExport, Editor);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    // Add event listener for requestNavigate event to customize hyperlink navigation functionality.
    requestNavigate = (args: RequestNavigateEventArgs) => {
        if (args.linkType !== 'Bookmark') {
            let link: string = args.navigationLink;
            if (args.localReference.length > 0) {
                link += '#' + args.localReference;
            }
            //Navigate to the specified URL.
            window.open(link);
            args.isHandled = true;
        }
    };

    render() {
        return (
            <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableSfdtExport={true} enableEditor={true}
                requestNavigate={this.requestNavigate.bind(this)} />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Remove hyperlink

To remove link from hyperlink in the document, press Backspace key at the end of a hyperlink. By removing the link, it will be converted as plain text. You can use ‘removeHyperlink’ method of ‘Editor’ instance if the selection is in hyperlink. Refer to the following example.

```typescript
documenteditor.editor.removeHyperlink();
```

## Hyperlink dialog

Document Editor provides dialog support to insert or edit a hyperlink. Refer to the following example.

{% tab template="document-editor/link" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, HyperlinkDialog
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(Selection, SfdtExport, Editor, HyperlinkDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    //Click the hyperlink button, the hyperlink dialog will open
    showHyperlinkDialog(): void {
        //Open hyperlink dialog.
        this.documenteditor.showDialog('Hyperlink');
    }

    render() {
        return (
            <div>
                <button onClick={this.showHyperlinkDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableSfdtExport={true} enableEditor={true} enableHyperlinkDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

You can use the following keyboard shortcut to open the hyperlink dialog if the selection is in hyperlink.

| Key Combination | Description |
|-----------------|-------------|
|Ctrl + K | Open hyperlink dialog that allows you to create or edit hyperlink|

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Hyperlink dialog](../document-editor/dialog#hyperlink-dialog)
