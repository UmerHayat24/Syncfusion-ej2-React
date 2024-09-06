---
title: "Images"
component: "DocumentEditor"
description: "Learn the supported image types in React document editor and how to insert, resize, format images."
---

# Images

Document Editor supports common raster format images like PNG, BMP, JPEG, and GIF. You can insert an image file or online image in the document using the `insertImage()` method. Refer to the following sample code.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    DocumentEditorComponent, SfdtExport, Selection, Editor, ImageResizer, EditorHistory
} from '@syncfusion/ej2-react-documenteditor';


DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, ImageResizer, EditorHistory);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    insertPicture(): void {
        let pictureUpload: HTMLInputElement = document.getElementById("insertImageButton") as HTMLInputElement;
        pictureUpload.value = '';
        //Open file picker.
        pictureUpload.click();
    }

    onInsertImage(args: any): void {
        let proxy: any = this;
        if (navigator.userAgent.match('Chrome') || navigator.userAgent.match('Firefox') || navigator.userAgent.match('Edge') || navigator.userAgent.match('MSIE') || navigator.userAgent.match('.NET')) {
            if (args.target.files[0]) {
                //Get selected file.
                let path = args.target.files[0];
                let reader = new FileReader();
                reader.onload = function (frEvent: any) {
                    let base64String = frEvent.target.result;
                    let image = document.createElement('img');
                    image.addEventListener('load', function () {
                        //Insert image in Document Editor.
                        proxy.documenteditor.editor.insertImage(base64String, this.width, this.height);
                    })
                    image.src = base64String;
                };
                //Convert image into base64 string.
                reader.readAsDataURL(path);
            }
            //Safari does not Support FileReader Class
        } else {
            let image = document.createElement('img');
            image.addEventListener('load', function () {
                //Insert image in Document Editor.
                proxy.documenteditor.editor.insertImage(args.target.value);
            })
            image.src = args.target.value;
        }
    }
    render() {
        return (
            <div>
                <input type="file" id="insertImageButton" style={{ "position": "fixed", "left": "-110em" }} accept=".jpg,.jpeg,.png,.bmp" onChange={this.onInsertImage.bind(this)} />
                <button onClick={this.insertPicture.bind(this)}>Dialog</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableImageResizer={true} enableEditorHistory={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

Image files will be internally converted to base64 string. Whereas, online images are preserved as URL.

## Image resizing

Document Editor provides built-in image resizer that can be injected into your application based on the requirements. This allows you to resize the image by dragging the resizing points using mouse or touch interactions. This resizer appears as follows.

![Image](images/image.png)

## Changing size

Document Editor expose API to get or set the size of the selected image. Refer to the following sample code.

```typescript
documenteditor.selection.imageFormat.width = 800;
documenteditor.selection.imageFormat.height = 800;
```

>Note: Images are stored and processed(read/write) as base64 string in DocumentEditor. The online image URL is preserved as a URL in DocumentEditor upon saving.

## Text wrapping style

Text wrapping refers to how images fit with surrounding text in a document. Please [refer to this page](../document-editor/text-wrapping-style) for more information about text wrapping styles available in Word documents.

## Positioning the image

DocumentEditor preserves the position properties of the image and displays the image based on position properties. It does not support modifying the position properties. Whereas the image will be automatically moved along with text edited if it is positioned relative to the line or paragraph.

## See Also

* [Feature modules](../document-editor/feature-module/)