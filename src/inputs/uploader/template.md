---
title: "Template"
component: "Uploader"
description: "Explains how to customize the file list with action buttons using a template that helps to design own user interface in the file upload control."
---

# Template

You can customize the default appearance of the uploader using a template along with buttons.

## File list template

The **template**property is used to customize the default appearance of each file in the list.
It can be represented as the HTML element or string. The selected or dropped files are displayed as per the template layout
provided. The remove and progress bar action is handled using the corresponding events when the template is defined.

For example, you can display file type icon along with the default UI elements.

{% tab template="uploader/filelist-template", sourceFiles="app/**/*.tsx, style.css" %}

```typescript

import {  detach, select } from '@syncfusion/ej2-base';
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
        public dropAreaClick(args: React.MouseEvent): void {
            const target: any = args.target as HTMLElement;
        if (target.classList.contains('e-file-delete-btn')) {
            for (const i of  this.uploadObj.getFilesData()) {
                if (target.closest('li').getAttribute('data-file-name') === i.name) {
                    this.uploadObj.remove(this.uploadObj.getFilesData()[this.uploadObj.getFilesData().indexOf(i)]);
                }
            }
        } else if (target.classList.contains('e-file-remove-btn')) {
            detach(target.closest('li'));
        }
        }
        public browseClick(args: React.MouseEvent): any {
          const wrapperEle: HTMLElement = select('.e-file-select-wrap button', document) as HTMLElement;
          wrapperEle.click();
          args.preventDefault();
        }

        public onFileUpload(args: any): void {
            const li: HTMLElement = this.dropAreaRef.querySelector('[data-file-name="' + args.file.name + '"]') as any;
            const progressValue: number = Math.round((args.e.loaded / args.e.total) * 100);
            li.getElementsByTagName('progress')[0].value = progressValue;
            li.getElementsByClassName('percent')[0].textContent = progressValue.toString() + " %";
        }
        public onuploadSuccess(args: any): void {
            if (args.operation === 'remove') {
                let height: any = this.dropAreaRef.style.height;
                height = (parseInt(height, 10) - 40) + 'px';
                this.dropAreaRef.style.height = height;
            } else {
                const li: HTMLElement = this.dropAreaRef.querySelector('[data-file-name="' + args.file.name + '"]') as any;
                const progressBar: HTMLElement = li.getElementsByTagName('progress')[0];
                progressBar.classList.add('e-upload-success');
                li.getElementsByClassName('percent')[0].classList.add('e-upload-success');
                const height: any = this.dropAreaRef.style.height;
                this.dropAreaRef.style.height = parseInt(height, 10) - 15 + 'px';
            }
        }
        public onSelect(args: SelectedEventArgs): void {
            const length: number = args.filesData.length;
            let height: any = this.dropAreaRef.style.height;
            height = parseInt(height, 10) + (length * 55) + 'px';
            this.dropAreaRef.style.height = height;
        }
        public onuploadFailed(args: any): void {
            const li: HTMLElement = this.dropAreaRef.querySelector('[data-file-name="' + args.file.name + '"]') as any;
            const progressBar: HTMLElement = li.getElementsByTagName('progress')[0];
            progressBar.classList.add('e-upload-failed');
            li.getElementsByClassName('percent')[0].classList.add('e-upload-failed');
        }
        public uploaderTemplate(data: any): JSX.Element {
        return (
            <div>
            <span className='wrapper'>
                <span className={'icon template-icons sf-icon-${data.type}'} />
                <span className='name file-name'>{data.name}</span>
            </span>
                <span className='file-size-td file-size'>{data.size} bytes</span>
                <span className='e-icons e-file-remove-btn' title='Remove' /> <br/>
                <progress id='progressBar' className='progressbar' value='0' max='100' />
                <span className='percent-td percent' />
            </div>);
        }

        public render(): JSX.Element{
            return (
                <div id='dropArea' onClick={this.dropAreaClick = this.dropAreaClick.bind(this)} ref={dropEle => {this.dropAreaRef = dropEle!}}>
                <span id='drop'> Drop files here or <a href="" id='browse' onClick={this.browseClick = this.browseClick.bind(this)}><u>Browse</u></a> </span>
                <UploaderComponent id='UploadFiles'  ref = {upload => {this.uploadObj = upload !}} asyncSettings={this.path}
                progress={this.onFileUpload = this.onFileUpload.bind(this)} selected={this.onSelect = this.onSelect.bind(this)} success={this.onuploadSuccess = this.onuploadSuccess.bind(this)} failure={this.onuploadFailed = this.onuploadFailed.bind(this)} template={this.uploaderTemplate} created={this.onCreated = this.onCreated.bind(this)}/>
            </div>);
        }
}
ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## Custom template

You can design the own template by preventing the default file list including buttons. When you use custom template to upload or remove the files, pass the custom UI argument as true
to call `upload`/`remove` public method as follows:

* UploaderObj.**upload**(filesData, true);

* UploaderObj.**remove**(filesData, true);

Refer to the following code sample.

{% tab template="uploader/custom-template", sourceFiles="app/**/*.tsx, style.css" %}

```typescript

import {  createElement, detach, EventHandler, select } from '@syncfusion/ej2-base';
import { FileInfo, RemovingEventArgs, SelectedEventArgs, UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public uploadObj: UploaderComponent;
     public parentElement : HTMLElement; public proxy : any; public progressbarContainer : HTMLElement;
     public filesDetails : FileInfo[] = [];
     public filesList: HTMLElement[] = [];
     public path: object = {
       removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove/',
       saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save/'
     }
     public dropAreaEle: HTMLElement;
     public dropAreaRef: HTMLElement;
     constructor(props: any) {
         super(props)
         this.removeFiles = this.removeFiles.bind(this);
     }

     public onCreated(): void {
           this.uploadObj.dropArea = this.dropAreaRef;
           this.uploadObj.dataBind();
       }
     public browseClick(args: React.MouseEvent): any {
         const wrapperEle: HTMLElement = select('.e-file-select-wrap button', document) as HTMLElement;
         wrapperEle.click();
         args.preventDefault();
     }
     public onSuccess(args: any) : void {
       const li: any =  this.dropAreaRef.querySelector('[data-file-name="' + args.file.name + '"]') as HTMLElement;
       if (args.operation === 'upload') {
           li.querySelector('.close-icon-container').classList.add('delete-icon');
           detach(li.getElementsByTagName('progress')[0]);
           (li.querySelector('.file-size') as HTMLElement).style.display = 'inline-block';
           (li.querySelector('.file-name') as HTMLElement).style.color = 'green';
       } else {
           this.uploadObj.element.value = '';
           detach(li);
       }
       EventHandler.add(li.querySelector('.close-icon-container'), 'click', this.removeFiles, this);
     }

       public onFileSelect(args : SelectedEventArgs) : void  {
         if ((this.dropAreaRef.querySelector('.upload-list-root')) === null) {
             this.parentElement = createElement('div', { className: 'upload-list-root' });
             this.parentElement.appendChild(createElement('ul', {className: 'ul-element' }));
            this.dropAreaRef.appendChild(this.parentElement);
         }
         for (const i of args.filesData) {
             this.formSelectedData(i, this);  // create the LI element for each file Data
         }
         this.filesDetails = this.filesDetails.concat(args.filesData);
         this.uploadObj.upload(args.filesData, true);
         args.cancel = true;
     }

    public formSelectedData ( selectedFiles : FileInfo, proxy: any ) : void {
         const liEle : any = createElement('li',  { className: 'file-lists', attrs: {'data-file-name' : selectedFiles.name} });
         liEle.appendChild(createElement('span', {className: 'file-name ', innerHTML: selectedFiles.name }));
         liEle.appendChild(createElement('span', {className: 'file-size ', innerHTML: this.uploadObj.bytesToSize(selectedFiles.size) }));
         if (selectedFiles.statusCode === '1') {
             this.progressbarContainer = createElement('span', {className: 'progress-bar-container'});
             this.progressbarContainer.appendChild(createElement('progress', {className: 'progress', attrs: {value : '0', max : '100'}} ));
             liEle.appendChild(this.progressbarContainer);
         } else { liEle.querySelector('.file-name').classList.add('upload-fails'); }
         const closeIconContainer : HTMLElement = createElement('span', {className: 'e-icons close-icon-container'});
         EventHandler.add(closeIconContainer, 'click', this.removeFiles, proxy);
         liEle.appendChild(closeIconContainer);
         (document as any).querySelector('.ul-element').appendChild(liEle);
         this.filesList.push(liEle);
     }

    public onFileUpload(args : any) : void {
         const li : any = this.dropAreaRef.querySelector('[data-file-name="' + args.file.name + '"]');
         EventHandler.remove(li.querySelector('.close-icon-container'), 'click', this.removeFiles);
         const progressValue : number = Math.round((args.e.loaded / args.e.total) * 100);
         if (!isNaN(progressValue)) {
             li.getElementsByTagName('progress')[0].value = progressValue;   // Updating the progress bar value
         }
     }
     public onUploadFailed(args : any) : void {
         const li : any = this.dropAreaRef.querySelector('[data-file-name="' + args.file.name + '"]');
         EventHandler.add(li.querySelector('.close-icon-container'), 'click', this.removeFiles, this);
         li.querySelector('.file-name ').classList.add('upload-fails');
         if (args.operation === 'upload') {
             detach(li.querySelector('.progress-bar-container'));
         }
     }
     public removeFiles(args : React.MouseEvent) : void {
         const status : string = this.filesDetails[this.filesList.indexOf((args.currentTarget as HTMLElement).parentElement as HTMLElement)].statusCode;
         if (status === '2') {
             this.uploadObj.remove(this.filesDetails[this.filesList.indexOf((args.currentTarget as HTMLElement).parentElement as HTMLElement)]);
         } else {
             detach((args.currentTarget as HTMLElement).parentElement as HTMLElement);
         }
     }
       public onFileRemove(args: RemovingEventArgs): void {
           args.postRawFile = false;
       }
     public render():JSX.Element{
       return (
         <div id='dropArea' className='dropArea' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
           <span id='drop' className='file-name-span drop'> Drop files here or <a href="" id='browse' onClick={this.browseClick = this.browseClick.bind(this)}><u>Browse</u></a> </span>
             <UploaderComponent id='fileUpload' type = 'file' ref = {upload => {this.uploadObj = upload !}}
               asyncSettings = {this.path}
               success={ this.onSuccess = this.onSuccess.bind(this) }
               selected= { this.onFileSelect = this.onFileSelect.bind(this) }
               progress = {this.onFileUpload = this.onFileUpload.bind(this) }
               failure = { this.onUploadFailed = this.onUploadFailed.bind(this) } created={this.onCreated = this.onCreated.bind(this)} removing={this.onFileRemove = this.onFileRemove.bind(this)}/>
         </div>);
       }
   }

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.

## See Also

* [Customize progress bar](./how-to/customize-progressbar)
* [Customize button with HTML element](./how-to/customize-button-with-html-element)
* [Customize drop area](./how-to/hide-default-drop-area)
