---
title: "Achieve invisible upload"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Achieve invisible upload

You can achieve the invisible upload feature by using the selected event in uploader component. Refer to the following example.

{% tab template="uploader/invisible", sourceFiles="app/**/*.tsx,style.css" %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
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
  private previewRef: HTMLElement;
  public onCreated(): void {
      this.uploadObj.dropArea = this.dropAreaRef;
      this.uploadObj.dataBind();
  }
  public onupload(args: SelectedEventArgs){
  for(const i of args.filesData){
          const liparentDiv = createElement('div',  { className: 'image-list'});
          const liImage = createElement('img',  { className: 'image'});
          liparentDiv.appendChild(liImage);
          this.readURL(liImage, i);
          this.previewRef.appendChild(liparentDiv);
      }
      args.cancel=true;

  }
  public readURL(liImage: HTMLElement, file: any): void {
      const imgPreview: HTMLImageElement = liImage as HTMLImageElement;
      const imageFile: File = file.rawFile;
      const reader: FileReader = new FileReader();
      reader.addEventListener( 'load', () => {
          imgPreview.src = reader.result as string;
      }, false);
      if (imageFile) {
          reader.readAsDataURL(imageFile);
      }
  };
  public render(): JSX.Element {
    return (
        <div className = 'control-pane'  ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
        <div className='control-section row uploadpreview'>
        <div className='col-lg-9'>
        <div className='upload_wrapper'>
        <div id='preview' ref={previewEle => this.previewRef = previewEle!}/>
            {/* Render Uploader */}
            <UploaderComponent id='fileUpload' type='file' ref = {upload => {this.uploadObj = upload !}}
            asyncSettings = {this.path}
            selected={ this.onupload=this.onupload.bind(this)} locale= {'en-US'} allowedExtensions= '.png, .jpg, .jpeg' created={this.onCreated = this.onCreated.bind(this)} />
        </div>
        </div>
        </div>
      </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
