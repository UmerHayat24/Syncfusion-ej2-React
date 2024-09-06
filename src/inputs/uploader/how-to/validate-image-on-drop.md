---
title: "Validate image on drop"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Validate image/* on drop

The uploader component allows you to upload all type of images by setting
**image/* ** to [allowedExtensions](../../api/uploader/#allowedextensions) property.

By default, the behavior is working with select a file using browse button. But, this behavior doesn’t support
on drag and drop the files. You can handle this behavior manually using `selected` event by filtering the file types from application.

In the following example, validated image files using images/*. You are able to drag and drop the image files with extension of PNG, JPG, BPG, GIF and TIFF to upload it.

{% tab template="uploader/validate-image", sourceFiles="app/**/*.tsx,style.css" %}

```typescript
import { SelectedEventArgs, UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
   public uploadObj: UploaderComponent;
  public path: object = {
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  private dropAreaRef: HTMLElement;
  public onCreated(): void {
      this.uploadObj.dropArea = this.dropAreaRef;
      this.uploadObj.dataBind();
  }
  public onSelected(args: SelectedEventArgs): void {
    if (args.event.type === 'drop') {
        const allImages = ['png', 'jpg', 'jpeg', 'gif', 'tiff', 'bpg'];
        const files = args.filesData;
        const modifiedFiles = [];
        for (const file of files) {
            if (allImages.indexOf(file.type) === -1) {
                file.status = 'File type is not allowed';
                file.statusCode = '0';
            }
            modifiedFiles.push(file);
        }
        args.isModified = true;
    }
  }
  public render(): JSX.Element {
        return (
            <div className = 'control-pane' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
                <div className='control-section row uploadpreview'>
                <div className='col-lg-9'>
                <div className='upload_wrapper'>
                    {/* Render Uploader */}
                    <UploaderComponent id='fileUpload' autoUpload = {false} type='file' ref = {upload => {this.uploadObj = upload !}}
                    asyncSettings = {this.path}
                    selected={ this.onSelected = this.onSelected.bind(this)} created={this.onCreated = this.onCreated.bind(this)} />
                </div>
                </div>
                </div>
        </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.