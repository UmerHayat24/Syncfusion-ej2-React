---
title: "Scrolling"
component: "DocumentEditor"
description: "Learn scrolling and zooming can be customized in React document editor."
---

# Scrolling

The Document Editor renders the document as page by page. You can scroll through the pages by mouse wheel or touch interactions. You can also scroll through the page by using ‘scrollToPage()’ method of document editor instance. Refer to the following code example.

{% tab template="document-editor/scrolling-zooming" compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent

} from '@syncfusion/ej2-react-documenteditor';

export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    onLoadDefault(): void {
        let defaultDocument: object = {
            sections: [
                {
                    blocks: [
                        {
                            paragraphFormat: {
                                styleName: 'Normal',
                            },
                            inlines: [
                                {
                                    text: 'First page',
                                },
                            ],
                        },
                    ],
                    headersFooters: {},
                },
                {
                    blocks: [
                        {
                            paragraphFormat: {
                                styleName: 'Normal',
                            },
                            inlines: [
                                {
                                    text: 'Second page',
                                },
                            ],
                        },
                    ],
                    headersFooters: {},
                },
            ],
            characterFormat: {},
            paragraphFormat: {},
            background: {
                color: '#FFFFFFFF',
            },
            styles: [
                {
                    type: 'Paragraph',
                    name: 'Normal',
                    next: 'Normal',
                },
                {
                    type: 'Character',
                    name: 'Default Paragraph Font',
                },
            ],
        };
        this.documenteditor.open(JSON.stringify(defaultDocument));
        this.documenteditor.focusIn();
    }

    public componentDidMount(): void {
        setTimeout(() => {
            //Load default document.
            this.onLoadDefault();
            //Scroll to specified page.
            this.documenteditor.scrollToPage(2);
        });
    }
    render() {
        return (
            <DocumentEditorComponent id="DocumentEditor" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

> Calling this method brings the specified page into view but doesn’t move selection. Hence this method will work by default. That is, it works even if selection is not enabled.

In case, if you wish to move the selection to any page in document editor and bring it into view, you can use ‘goToPage()’ method of selection instance. Refer to the following code example.

{% tab template="document-editor/scrolling-zooming" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog,
} from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    onLoadDefaultDocument(): void {
        let defaultDocument: object = {
            sections: [
                {
                    blocks: [
                        {
                            paragraphFormat: {
                                styleName: 'Normal',
                            },
                            inlines: [
                                {
                                    text: 'First page',
                                },
                            ],
                        },
                    ],
                    headersFooters: {},
                },
                {
                    blocks: [
                        {
                            paragraphFormat: {
                                styleName: 'Normal',
                            },
                            inlines: [
                                {
                                    text: 'Second page',
                                },
                            ],
                        },
                    ],
                    headersFooters: {},
                },
                {
                    blocks: [
                        {
                            paragraphFormat: {
                                styleName: 'Normal',
                            },
                            inlines: [
                                {
                                    text: 'Third page',
                                },
                            ],
                        },
                    ],
                    headersFooters: {},
                },
            ],
            characterFormat: {},
            paragraphFormat: {},
            background: {
                color: '#FFFFFFFF',
            },
            styles: [
                {
                    type: 'Paragraph',
                    name: 'Normal',
                    next: 'Normal',
                },
                {
                    type: 'Character',
                    name: 'Default Paragraph Font',
                },
            ],
        };
        this.documenteditor.open(JSON.stringify(defaultDocument));
        this.documenteditor.focusIn();
    }

    public componentDidMount(): void {
        setTimeout(() => {
            //Load default document.
            this.onLoadDefaultDocument();
            //Navigate to specified page.
            this.documenteditor.viewer.selection.goToPage(3);
        });
    }
    render() {
        return (
            <DocumentEditorComponent
                id="container"
                height={'330px'}
                ref={(scope) => {
                    this.documenteditor = scope;
                }}
                isReadOnly={false}
                enablePrint={true}
                enableSelection={true}
                enableEditor={true}
                enableEditorHistory={true}
                enableContextMenu={true}
                enableSearch={true}
                enableOptionsPane={true}
                enableBookmarkDialog={true}
                enableBordersAndShadingDialog={true}
                enableFontDialog={true}
                enableTableDialog={true}
                enableParagraphDialog={true}
                enableHyperlinkDialog={true}
                enableImageResizer={true}
                enableListDialog={true}
                enablePageSetupDialog={true}
                enableSfdtExport={true}
                enableStyleDialog={true}
                enableTableOfContentsDialog={true}
                enableTableOptionsDialog={true}
                enableTablePropertiesDialog={true}
                enableTextExport={true}
                enableWordExport={true}
            />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Zooming

You can scale the contents in document editor ranging from 10% to 500% of the actual size. You can achieve this using mouse or touch interactions. You can also use ‘zoomFactor’ property of document editor instance. The value can be specified in a range from 0.1 to 5. Refer to the following code example.

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, Print, SfdtExport, WordExport, TextExport,
    Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane,
    HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog,
    ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog,
    BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog,
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);

export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        //Set zoom factor.
        this.documenteditor.zoomFactor = 3;
    }
    render() {
        return (
            <DocumentEditorComponent id="container" ref={(scope) => { this.documenteditor = scope; }} height={'330px'} style={{
                width: '100%'
            }} isReadOnly={false} enablePrint={true} enableSelection={true} enableEditor={true} enableEditorHistory={true} enableContextMenu={true} enableSearch={true} enableOptionsPane={true} enableBookmarkDialog={true} enableBordersAndShadingDialog={true} enableFontDialog={true} enableTableDialog={true} enableParagraphDialog={true} enableHyperlinkDialog={true} enableImageResizer={true} enableListDialog={true} enablePageSetupDialog={true} enableSfdtExport={true} enableStyleDialog={true} enableTableOfContentsDialog={true} enableTableOptionsDialog={true} enableTablePropertiesDialog={true} enableTextExport={true} enableWordExport={true} />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));
```

{% endtab %}

## Page Fit Type

Apart from specifying the zoom factor as value, the Document Editor provides option to specify page fit options such as fit to full page or fit to page width. You can set this option using ‘fitPage’ method of document editor instance. Refer to the following code example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, DocumentEditor, Print, SfdtExport, WordExport, TextExport,
    Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane,
    HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog,
    ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog,
    BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog,
} from '@syncfusion/ej2-react-documenteditor';

DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog,  BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
  public documenteditor: DocumentEditorComponent;

  public componentDidMount(): void {
    this.documenteditor.fitPage('FitPageWidth');
  }
  render() {
    return (
       <DocumentEditorComponent id="container" ref={(scope) => { this.documenteditor = scope; }} height={'330px'} style={{ width: '100%' }} isReadOnly={false} enablePrint={true} enableSelection={true} enableEditor={true} enableEditorHistory={true} enableContextMenu={true} enableSearch={true} enableOptionsPane={true} enableBookmarkDialog={true} enableBordersAndShadingDialog={true} enableFontDialog={true} enableTableDialog={true} enableParagraphDialog={true} enableHyperlinkDialog={true} enableImageResizer={true} enableListDialog={true} enablePageSetupDialog={true} enableSfdtExport={true} enableStyleDialog={true} enableTableOfContentsDialog={true} enableTableOptionsDialog={true} enableTablePropertiesDialog={true} enableTextExport={true}  enableWordExport={true} />
    );
  }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Zoom option using UI

The following code example shows how to provide zoom options in document editor.

{% tab template="document-editor/scrolling-zooming" compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog } from '@syncfusion/ej2-react-documenteditor';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';

//Inject require module.
DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    public pageCount;
    public editablePageNumber;
    public editorPageCount;
    public pageNumberLabel;
    public startPage = 1;
    public zoom;
    public items: ItemModel[] = [
        {
            text: '200%',
        },
        {
            text: '175%',
        },
        {
            text: '150%',
        },
        {
            text: '125%',
        },
        {
            text: '100%',
        },
        {
            text: '75%',
        },
        {
            text: '50%',
        },
        {
            text: '25%',
        },
        {
            separator: true,
        },
        {
            text: 'Fit one page',
        },
        {
            text: 'Fit page width',
        },
    ];
    public componentDidMount(): void {
        let instance: any = this;
        instance.pageCount = document.getElementById('documenteditor_pagecount');
        instance.editablePageNumber = document.getElementById('editablePageNumber');
        instance.pageNumberLabel = document.getElementById(
            'documenteditor_page_no'
        );

        instance.updatePageCount();
        instance.updatePageNumber();
        instance.documenteditor.viewChange = function (e) {
            instance.updatePageNumberOnViewChange(e);
        };
        instance.documenteditor.contentChange = function () {
            instance.updatePageCount();
        };
        instance.editablePageNumber.onclick = function () {
            instance.updateDocumentEditorPageNumber();
        };
        instance.editablePageNumber.onkeydown = function (e) {
            instance.onKeyDown(e);
        };
        instance.editablePageNumber.onblur = function () {
            instance.onBlur();
        };
    }

    updatePageNumberOnViewChange(args) {
        if (
            this.documenteditor.selection &&
            this.documenteditor.selection.startPage >= args.startPage &&
            this.documenteditor.selection.startPage <= args.endPage
        ) {
            this.startPage = this.documenteditor.selection.startPage;
        } else {
            this.startPage = args.startPage;
        }
        this.updatePageNumber();
    }
    onBlur() {
        if (
            this.editablePageNumber.textContent === '' ||
            parseInt(this.editablePageNumber.textContent, 0) > this.editorPageCount
        ) {
            this.updatePageNumber();
        }
        this.editablePageNumber.contentEditable = 'false';
    }
    onKeyDown(e) {
        if (e.which === 13) {
            e.preventDefault();
            var pageNumber = parseInt(this.editablePageNumber.textContent, 0);
            if (pageNumber > this.editorPageCount) {
                this.updatePageNumber();
            } else {
                if (this.documenteditor.selection) {
                    this.documenteditor.selection.goToPage(
                        parseInt(this.editablePageNumber.textContent, 0)
                    );
                } else {
                    this.documenteditor.scrollToPage(
                        parseInt(this.editablePageNumber.textContent, 0)
                    );
                }
            }
            this.editablePageNumber.contentEditable = 'false';
            if (this.editablePageNumber.textContent === '') {
                this.updatePageNumber();
            }
        }
        if (e.which > 64) {
            e.preventDefault();
        }
    }
    onZoom(args) {
        this.setZoomValue(args.item.text);
        this.updateZoomContent();
    }
    setZoomValue(text) {
        if (text.match('Fit one page')) {
            this.documenteditor.fitPage('FitOnePage');
        } else if (text.match('Fit page width')) {
            this.documenteditor.fitPage('FitPageWidth');
        } else {
            this.documenteditor.zoomFactor = parseInt(text, 0) / 100;
        }
    }
    updateZoomContent() {
        this.zoom.content = Math.round(this.documenteditor.zoomFactor * 100) + '%';
    }
    updatePageNumber() {
        this.pageNumberLabel.textContent = this.startPage.toString();
    }
    updatePageCount() {
        this.editorPageCount = this.documenteditor.pageCount;
        this.pageCount.textContent = this.editorPageCount.toString();
    }
    updateDocumentEditorPageNumber() {
        let editPageNumber = document.getElementById('editablePageNumber');
        editPageNumber.contentEditable = 'true';
        editPageNumber.focus();
        window.getSelection().selectAllChildren(editPageNumber);
    }
    render() {
        return (
            <div>
                <DocumentEditorComponent
                    id="container"
                    height={'330px'}
                    ref={(scope) => {
                        this.documenteditor = scope;
                    }}
                    isReadOnly={false}
                    enablePrint={true}
                    enableSelection={true}
                    enableEditor={true}
                    enableEditorHistory={true}
                    enableContextMenu={true}
                    enableSearch={true}
                    enableOptionsPane={true}
                    enableBookmarkDialog={true}
                    enableBordersAndShadingDialog={true}
                    enableFontDialog={true}
                    enableTableDialog={true}
                    enableParagraphDialog={true}
                    enableHyperlinkDialog={true}
                    enableImageResizer={true}
                    enableListDialog={true}
                    enablePageSetupDialog={true}
                    enableSfdtExport={true}
                    enableStyleDialog={true}
                    enableTableOfContentsDialog={true}
                    enableTableOptionsDialog={true}
                    enableTablePropertiesDialog={true}
                    enableTextExport={true}
                    enableWordExport={true}
                />
                <div id="page-fit-type-div">
                    <label id='page' > Page </label>
                    <div id="editablePageNumber">
                        <label id="documenteditor_page_no" />
                    </div>
                    <label id="of">of</label>
                    <label id="documenteditor_pagecount" />
                    <DropDownButtonComponent ref={scope => { this.zoom = scope; }} items={this.items} cssClass="e-de-statusbar-zoom" select={this.onZoom.bind(this)}                    >                        100%          </DropDownButtonComponent>
                </div>
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}
