---
title: "How to disable optimized text measuring approach"
component: "DocumentEditor"
description: "Learn how to disable optimized text measuring approach in Document Editor and retain the document pagination behavior like v19.2.0.x and older versions."
---

# How to disable optimized text measuring in React Document Editor component

Starting from v19.3.0.x, the accuracy of text size measurements in Document editor is improved such as to match Microsoft Word pagination for most Word documents. This improvement is included as default behavior along with an optional API `enableOptimizedTextMeasuring` in Document editor settings.  

If you want the Document editor component to retain the document pagination (display page-by-page) behavior like v19.2.0.x and older versions. Then you can disable this optimized text measuring improvement, by setting `false` to [`enableOptimizedTextMeasuring`](../../api/document-editor/documentEditorSettingsModel/#enableoptimizedtextmeasuring) property of  React Document Editor component.

## Disable optimized text measuring in `DocumentEditorContainer` instance

The following example code illustrates how to disable optimized text measuring improvement in `DocumentEditorContainer` instance.

```typescript
import * as React from 'react';
import { DocumentEditorContainerComponent, Toolbar } from '@syncfusion/ej2-react-documenteditor';

DocumentEditorContainerComponent.Inject(Toolbar);

export default class App extends React.Component {

  // Disable optimized text measuring improvement  
  public settings = { enableOptimizedTextMeasuring: false };

  render() {
    return (
      <DocumentEditorContainerComponent
        id="container"
        style={{ height: '590px' }}
        serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/"
        enableToolbar={true}
        documentEditorSettings={this.settings}
      />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

## Disable optimized text measuring in `DocumentEditor` instance

The following example code illustrates how to disable optimized text measuring improvement in `DocumentEditor` instance.

```typescript



import * as ReactDOM from 'react-dom';
import * as React from 'react';

import {
    DocumentEditorComponent, DocumentEditor, RequestNavigateEventArgs, ViewChangeEventArgs,
    Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory,
    ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog,
    PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog,
    TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(Print, SfdtExport, WordExport, TextExport, Selection, Search, Editor, ImageResizer, EditorHistory, ContextMenu, OptionsPane, HyperlinkDialog, TableDialog, BookmarkDialog, TableOfContentsDialog, PageSetupDialog, StyleDialog, ListDialog, ParagraphDialog, BulletsAndNumberingDialog, FontDialog, TablePropertiesDialog, BordersAndShadingDialog, TableOptionsDialog, CellOptionsDialog, StylesDialog);
export class Default extends React.Component<{}, {}> {
  // Disable optimized text measuring improvement
  public settings = { enableOptimizedTextMeasuring: false };

    render() {
        return (
            <DocumentEditorComponent id="container" height={'330px'} serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/" isReadOnly={false} enablePrint={true}
                enableSelection={true} enableEditor={true} enableEditorHistory={true}
                enableContextMenu={true} enableSearch={true} enableOptionsPane={true}
                enableBookmarkDialog={true} enableBordersAndShadingDialog={true} enableFontDialog={true} enableTableDialog={true} enableParagraphDialog={true} enableHyperlinkDialog={true} enableImageResizer={true} enableListDialog={true}
                enablePageSetupDialog={true} enableSfdtExport={true}
                enableStyleDialog={true} enableTableOfContentsDialog={true}
                enableTableOptionsDialog={true} enableTablePropertiesDialog={true}
                enableTextExport={true} enableWordExport={true} documentEditorSettings={this.settings} />
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```