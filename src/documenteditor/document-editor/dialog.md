---
title: "Dialog"
component: "DocumentEditor"
description: "Learn the built-in dialog support in React document editor and how to open it."
---

# Dialog

Document Editor provides dialog support to major operations such as insert or edit hyperlink, formatting text, paragraph, style, list and table properties.

## Font Dialog

Font dialog allows you to modify all text properties for selected contents at once such as bold, italic, underline, font size, font color, strikethrough, subscript and superscript.

>Document Editor features are segregated into individual feature-wise modules. To use font Dialog, inject ‘FontDialog’ module using the ‘DocumentEditor.Inject(Selection, SfdtExport, Editor, FontDialog)’.
>To enable font dialog for a document editor instance, set ‘enableFontDialog’ to true.

Refer to the following example.

{% tab template="document-editor/dialog" compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor, FontDialog } from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, FontDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showFontDialog(): void {
        //Open font dialog.
        this.documenteditor.showDialog('Font');
    }
    render() {
        return (
            <div>
                <button onClick={this.showFontDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableFontDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));
```

{% endtab %}

## Paragraph dialog

This dialog allows modifying the paragraph formatting for selection at once such as text alignment, indentation, and spacing.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor, ParagraphDialog } from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, ParagraphDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showParagraphDialog(): void {
        //Open paragraph dialog.
        this.documenteditor.showDialog('Paragraph');
    }
    render() {
        return (
            <div>
                <button onClick={this.showParagraphDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableParagraphDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Table dialog

This dialog allows creating and inserting a table at cursor position by specifying the required number of rows and columns.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, TableDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, TableDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showTableDialog(): void {
        //Open table dialog.
        this.documenteditor.showDialog('Table');
    }
    render() {
        return (
            <div>
                <button onClick={this.showTableDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableTableDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Bookmark dialog

This dialog allows you to perform the following operations:

* View all bookmarks.
* Navigate to a bookmark.
* Create a bookmark at current selection.
* Delete an existing bookmark.
To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, BookmarkDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, BookmarkDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showBookmarkDialog(): void {
        //Open bookmark dialog.
        this.documenteditor.showDialog('Bookmark');
    }
    render() {
        return (
            <div>
                <button onClick={this.showBookmarkDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableBookmarkDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Hyperlink dialog

This dialog allows editing or inserting a hyperlink at cursor position.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, HyperlinkDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, HyperlinkDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showHyperlinkDialog(): void {
        //Open hyperlink dialog;
        this.documenteditor.showDialog('Hyperlink');
    }
    render() {
        return (
            <div>
                <button onClick={this.showHyperlinkDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableHyperlinkDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Table of contents dialog

This dialog allows creating and inserting table of contents at cursor position. If the table of contents already exists at cursor position, you can customize its properties.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, TableOfContentsDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, TableOfContentsDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showTableOfContentsDialog(): void {
        //Open table of contents dialog.
        this.documenteditor.showDialog('TableOfContents');
    }
    render() {
        return (
            <div>
                <button onClick={this.showTableOfContentsDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableTableOfContentsDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Styles Dialog

This dialog allows managing the styles in a document. It will display all the styles in the document with options to modify the properties of the existing style or create new style with the help of ‘Style dialog’. Refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, StyleDialog, StylesDialog
} from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, StyleDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showStylesDialog(): void {
        //Open styles dialog.
        this.documenteditor.showDialog('Styles');
    }
    render() {
        return (
            <div>
                <button onClick={this.showStylesDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableStylesDialog={true} enableStyleDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Style dialog

You can directly use this dialog for modifying any existing style or add new style by providing the style name.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, StyleDialog
} from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, StyleDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showStyleDialog(): void {
        //Open style dialog.
        this.documenteditor.showDialog('Style');
    }
    render() {
        return (
            <div>
                <button onClick={this.showStyleDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableStyleDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## List dialog

This dialog allows creating a new list or modifying existing lists in the document.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, ListDialog
} from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, ListDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showListDialog(): void {
        //Open list dialog.
        this.documenteditor.showDialog('List');
    }
    render() {
        return (
            <div>
                <button onClick={this.showListDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableListDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Borders and shading dialog

This dialog allows customizing the border style, border width, and background color of the table or selected cells.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, BordersAndShadingDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, BordersAndShadingDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        //Insert table
        this.documenteditor.editor.insertTable(2, 2);
    }

    showBordersAndShadingDialog(): void {
        //Open borders and shading dialog.
        this.documenteditor.showDialog('BordersAndShading');
    }
    render() {
        return (
            <div>
                <button onClick={this.showBordersAndShadingDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableBordersAndShadingDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Table options dialog

This dialog allows customizing the default cell margins and spacing between each cells of the selected table.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, TableOptionsDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, TableOptionsDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    public componentDidMount(): void {
        //Insert table.
        this.documenteditor.editor.insertTable(2, 2);
    }

    showTableOptionsDialog(): void {
        //Open table options dialog.
        this.documenteditor.showDialog('TableOptions');
    }
    render() {
        return (
            <div>
                <button onClick={this.showTableOptionsDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableTableOptionsDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Table properties dialog

This dialog allows customizing the table, row, and cell properties of the selected table.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, TableOptionsDialog, TablePropertiesDialog, BordersAndShadingDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, BordersAndShadingDialog, TableOptionsDialog, TablePropertiesDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        //Insert table.
        this.documenteditor.editor.insertTable(2, 2);
    }

    showTablePropertiesDialog(): void {
        //Open table properties dialog.
        this.documenteditor.showDialog('TableProperties');
    }
    render() {
        return (
            <div>
                <button onClick={this.showTablePropertiesDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableBordersAndShadingDialog={true} enableTableOptionsDialog={true} enableTablePropertiesDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## Page setup dialog

This dialog allows customizing margins, size, and layout options for pages of the section.

To open this dialog, refer to the following example.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, PageSetupDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, PageSetupDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    showPageSetupDialog(): void {
        //Open page setup dialog.
        this.documenteditor.showDialog('PageSetup');
    }
    render() {
        return (
            <div>
                <button onClick={this.showPageSetupDialog.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enablePageSetupDialog={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [Feature modules](../document-editor/feature-module/)
