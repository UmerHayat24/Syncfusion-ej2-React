---
title: "Add confirm dialog to remove the files"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Add confirm dialog to remove the files

You can customize the uploader component using confirm dialog before removing the files. Here, ej2 dialog is used as confirm dialog. Refer to the following example.

{% tab template="uploader/confirm-dialog", sourceFiles="app/**/*.tsx,style.css" %}

```typescript
import { FileInfo, SelectedEventArgs, UploaderComponent } from '@syncfusion/ej2-react-inputs';
import {DialogComponent} from '@syncfusion/ej2-react-popups';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public uploadObj: UploaderComponent;
  public dialog: DialogComponent;
  public removeFile: FileInfo[] = [];
  public path: object = {
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  private buttons: object = [{buttonModel: { content: 'OK', isPrimary:'true' },'click': () => { this.dialog.hide();
    this.uploadObj.remove(this.removeFile[0], false, true); }},
            {'click': () => {this.dialog.hide(); }, buttonModel: { content: 'Cancel', cssClass: 'e-flat'} }];
  private dropAreaRef: HTMLElement;
  public onCreated(): void {
      this.uploadObj.dropArea = this.dropAreaRef;
      this.uploadObj.dataBind();
  }
  public onremove(args: SelectedEventArgs) {
    this.removeFile=[];
    args.cancel = true;
    this.removeFile.push(args.filesData as any);
    this.dialog.show();
  }
    public render(): JSX.Element {
        return (
              <div className = 'control-pane' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
            <div className='control-section row uploadpreview'>
            <div className='col-lg-9'>
            <div className='upload_wrapper'>
            <div id='preview' />
                {/* Render Uploader */}
                <UploaderComponent id='fileUpload' type='file' ref = {upload => {this.uploadObj = upload !}}
                asyncSettings = {this.path}
                removing={this.onremove = this.onremove.bind(this)} created={this.onCreated = this.onCreated.bind(this)} />
                <div id='targetElement' style={{minHeight:'200px'}} />
                <DialogComponent id="defaultdialog" content={"Are you sure want to remove the file?"}  width={'300px'} ref={dialog => this.dialog = dialog !}
                target={'#targetElement'} visible={false} buttons={this.buttons}/>
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
