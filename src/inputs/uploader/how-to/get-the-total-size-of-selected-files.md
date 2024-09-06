---
title: "Get the total size of selected files"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Get the total size of selected files

You can get the total size of selected files before uploading it to the designated server. This can be achieved by using the selected event. Refer to the following example to calculate the total file size.

{% tab template="uploader/file-size", sourceFiles="app/**/*.tsx,style.css" %}

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
  public onSelect(args: SelectedEventArgs): void {
    let totalSize: number = 0;
    for (const file of args.filesData) {
        totalSize = totalSize + file.size;
    }
    const size: string = this.uploadObj.bytesToSize(totalSize);
    alert("Total select file's size is " + size);
  }

    public render(): JSX.Element {
        return (
        <div className = 'control-pane' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
      <div className='control-section row uploadpreview'>
      <div className='col-lg-9'>
      <div className='upload_wrapper'>
      <div id='preview' />
          <UploaderComponent id='fileUpload' type='file' ref = {upload => {this.uploadObj = upload !}}
          asyncSettings = {this.path}
          selected={ this.onSelect=this.onSelect.bind(this)} created={this.onCreated = this.onCreated.bind(this)} />
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
