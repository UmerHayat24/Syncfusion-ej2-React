---
title: " Rich text editor restricts the image uploading while uploading with large size"
component: "Rich Text Editor"
description: "This section for Syncfusion React Rich Text Editor control explains about, how to restrict the image to upload, when the given image size is greater than the allowed size"
---

# Restrict the image uploading while uploading with large size

By using the Rich text editor's `imageUploading` event, you can get the image size before uploading and restrict the image to upload, when the given image size is greater than the allowed size.

In the following, we have validated the image size before uploading and determined whether the image has been uploaded or not.

{% tab template="rich-text-editor/how-to-check-image-size", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

import { Count, HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

export class App extends React.Component<{},{}> {
private toolbarSettings: object = {
    items: ['Bold', 'Italic', 'Underline', 'StrikeThrough','|',
        'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
        'LowerCase', 'UpperCase', '|',
        'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
        'Outdent', 'Indent', '|',
        'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
        'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
};

private insertImageSettings: object = {
    saveUrl: "https://aspnetmvc.syncfusion.com/services/api/uploadbox/Save",
    path: "../Images/"
};

public onImageUploading = (args: any) => {
     console.log("file is uploading");
    let imgSize: number = 500000;
    let sizeInBytes: number = args.fileData.size;
    if ( imgSize < sizeInBytes ) {
        args.cancel = true;
    }

}

public render() {
    return (
      <RichTextEditorComponent toolbarSettings={this.toolbarSettings} insertImageSettings={this.insertImageSettings} imageUploading={this.onImageUploading.bind(this)} >
        <Inject services={[Toolbar, Count, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}