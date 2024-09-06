---
title: "How to"
component: "DocumentEditor"
description: "Learn how to change the document view to web layout and print view in document editor."
---

# Change document view

## How to change the document view in DocumentEditor component

Document Editor allows you to change the view to web layout and print using the [`layoutType`](../../api/document-editor#layouttype) property with the supported [`LayoutType`](../../api/document-editor/layouttype/).

```html
 <DocumentEditorComponent id="container" layoutType={'Continuous'} />
```

>Note: Default value of [`layoutType`](../../api/document-editor#layouttype) in Document Editor component is [`Pages`](../../api/document-editor/layoutType/).

## How to change the document view in DocumentEditorContainer component

Document Editor Container component allows you to change the view to web layout and print using the [`layoutType`](../../api/document-editor-container#layouttype) property with the supported [`LayoutType`](../../api/document-editor/layouttype/).

```html
<DocumentEditorContainerComponent id="container" layoutType={'Continuous'} enableToolbar={true}/>
```

>Note: Default value of [`layoutType`](../../api/document-editor-container#layouttype) in Document Editor Container component is [`Pages`](../../api/document-editor/layoutType/).