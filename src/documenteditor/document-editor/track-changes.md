---
title: "Track Changes"
component: "DocumentEditor"
description: "Learn use track changes in JavaScript document editor"
---

# Track Changes

Track Changes allows you to keep a record of changes or edits made to a document. You can then choose to accept or reject the modifications. It is a useful tool for managing changes made by several reviewers to the same document. If track changes option is enabled, all editing operations are preserved as revisions in Document Editor.

## Enable track changes in Document Editor

The following example demonstrates how to enable track changes.

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, DocumentEditor
} from '@syncfusion/ej2-react-documenteditor';

export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        this.documentEditor.spellChecker.languageID = 1033 //LCID of "en-us";
        this.documentEditor.spellChecker.removeUnderline = false;
        this.documentEditor.spellChecker.allowSpellCheckAndSuggestion = true;
    }

    render() {
        return (
            <DocumentEditorComponent id="container" ref={(scope) => { this.documenteditor = scope; }} enableTrackChanges={true}/>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));
```

## Get all tracked revisions

The following example demonstrate how to get all tracked revision from current document.

```typescript
<DocumentEditorComponent id="container" ref={(scope) => { this.documenteditor = scope; }} enableTrackChanges={true}/>
/**
 * Get revisions from the current document
 */
let revisions : RevisionCollection = this.container.documentEditor.revisions;
```

## Accept or Reject all changes programmatically

The following example demonstrates how to accept/reject all changes.

```typescript
<DocumentEditorComponent id="container" ref={(scope) => { this.documenteditor = scope; }} enableTrackChanges={true}/>
/**
 * Get revisions from the current document
 */
let revisions : RevisionCollection = this.container.documentEditor.revisions;
/**
 * Accept all tracked changes
 */
revisions.acceptAll();
/**
 * Reject all tracked changes
 */
revisions.rejectAll();
```

## Accept or reject a specific revision

The following example demonstrates how to accept/reject specific revision in the document editor.

```typescript
/**
 * Get revisions from the current document
 */
let revisions : RevisionCollection = this.container.documentEditor.revisions;
/**
 * Accept specific changes
 */
revisions.get(0).accept();
/**
 * Reject specific changes
 */
revisions.get(1).reject();
```

## Navigate between the tracked changes

The following example demonstrates how to navigate tracked revision programmatically.

```typescript
/**
 * Navigate to next tracked change from the current selection.
 */
this.container.documentEditor.selection.navigateNextRevision();
/**
 * Navigate to previous tracked change from the current selection.
 */
this.container.documentEditor.selection.navigatePreviousRevision();
```

## Filtering changes based on user

In DocumentEditor, we have built-in review panel in which we have provided support for filtering changes based on the user.

![Track changes](images/track-changes.png)