---
title: "Insert footnote endnote"
component: "DocumentEditor"
description: "Learn how to insert or edit footnotes and endnotes references in JavaScript document editor."
---

# Insert footnote endnote

DocumentEditorContainer component provides support for inserting footnotes and endnotes through the in-built toolbar. Refer to the following screenshot.

![Insert footnote endnote](images/note-toolbar.jpg)

The Footnotes and endnotes are both ways of adding extra bits of information to your writing outside of the main text. You can use footnotes and endnotes to add side comments to your work or to place other publications like books, articles, or websites.

## Insert footnotes

Document Editor exposes an API to insert footnotes at cursor position programmatically or can be inserted to the end of selected text.

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';

import {
    DocumentEditorComponent, Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory,
    ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog,
    PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog,
    TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog
} from '@syncfusion/ej2-react-documenteditor';

//Inject require module.
DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    Footnote(): void {
        //Insert footnote.
        this.documenteditor.editor.insertFootnote();
    }

    render() {
        return (
            <div>
                <button onClick={this.Footnote.bind(this)}>insert Footnote</button>
                <DocumentEditorComponent id="container" height={'330px'} serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/" isReadOnly={false} enablePrint={true}
                    enableSelection={true} enableEditor={true} enableEditorHistory={true}
                    enableContextMenu={true} enableSearch={true} enableOptionsPane={true}
                    enableBookmarkDialog={true} enableBordersAndShadingDialog={true} enableFontDialog={true} enableTableDialog={true} enableParagraphDialog={true} enableHyperlinkDialog={true} enableImageResizer={true} enableListDialog={true}
                    enablePageSetupDialog={true} enableSfdtExport={true}
                    enableStyleDialog={true} enableTableOfContentsDialog={true}
                    enableTableOptionsDialog={true} enableTablePropertiesDialog={true}
                    enableTextExport={true} enableWordExport={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

## Insert endnotes

Document Editor exposes an API to insert endnotes at cursor position programmatically or can be inserted to the end of selected text.

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';

import {
    DocumentEditorComponent, Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory,
    ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog,
    PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog,
    TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog
} from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
    private documenteditor: DocumentEditorComponent
    InsertEndnote(): void {
        //Insert end note.
        this.documenteditor.editor.insertEndnote();
    }

    render() {
        return (
            <div>
                <button onClick={this.InsertEndnote.bind(this)}>insert Endnote</button>
                <DocumentEditorComponent id="container" height={'330px'} serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/" isReadOnly={false} enablePrint={true}
                    enableSelection={true} enableEditor={true} enableEditorHistory={true}
                    enableContextMenu={true} enableSearch={true} enableOptionsPane={true}
                    enableBookmarkDialog={true} enableBordersAndShadingDialog={true} enableFontDialog={true} enableTableDialog={true} enableParagraphDialog={true} enableHyperlinkDialog={true} enableImageResizer={true} enableListDialog={true}
                    enablePageSetupDialog={true} enableSfdtExport={true}
                    enableStyleDialog={true} enableTableOfContentsDialog={true}
                    enableTableOptionsDialog={true} enableTablePropertiesDialog={true}
                    enableTextExport={true} enableWordExport={true} />
            </div>

        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));
```

## Update or edit footnotes and endnotes

You can update or edit the footnotes and endnotes using the built-in context menu shown up by right-clicking it.
the footnote endnote dialog box popup and you can customize the number format and start at. Refer to the following screenshot.

![Update or edit footnotes and endnotes](images/notes-option.jpg)
