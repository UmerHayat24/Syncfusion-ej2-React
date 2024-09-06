---
title: "React Rich Text Editor with image actions with upload"
component: "Rich Text Editor"
description: "The user guide section shows the option to insert images within your content with the caption, link, drag-and-drop images, image with the upload, and resize."
---

# Image

Rich Text Editor allows to insert images from online sources as well as local computer where you want to insert the image in your content. For inserting the image to the Rich Text Editor, the following list of options have been provided in the [insertImageSettings](/rich-text-editor/api-imageSettingsModel.html).

| **Options** | **Description** |
| --- | --- |
| allowedTypes | Specifies the extensions of the image types allowed to insert on bowering and passing the extensions with comma separators. <br /> <br /> For example, pass allowedTypes as .jpg and .png. |
| display | Sets the default display for an image when it is inserted into the Rich Text Editor. <br /><br /> Possible options are: 'inline' and 'block'. |
| width | Sets the default width of the image when it is inserted in the Rich Text Editor. |
| height | Sets the default height of the image when it is inserted in the Rich Text Editor. |
| saveUrl | Provides URL to map the action result method to save the image. |
| path | Specifies the location to store the image. |

> Rich Text Editor features are segregated into individual feature-wise modules. To use image and link tool, inject image module using the `RichTextEditor.Inject(image)`.

## Upload options

Through the ‘browse’ option, select the image from the local machine and insert into the Rich Text Editor content.

If the path field is not specified in the [insertImageSettings](/rich-text-editor/api-imageSettingsModel.html), the image will be transferred into base 64 and blob url for the image will be created and the generated url will be set to the src property of img tag.

```javascript
    <img src="blob:http://http.example.com/3ab56a6e-ec0d-490f-85a5-f0aeb0ad8879" >
```

> If you want to insert a lot of tiny images in the editor and don't want a specific physical location for saving images, you can opt to save format as Base64.

In the following sample, the image has been loaded from the local machine and it will be saved in the given location.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Image Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  private toolbarSettings: object = {
    items: ['Image']
  }

  public render() {
    return (
      <RichTextEditorComponent height={450} toolbarSettings={this.toolbarSettings}>
        <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
          Users can format their content using standard toolbar commands.</p>
        <p><b>Key features:</b></p>
        <ul>
          <li>
            <p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p>
          </li>
          <li>
            <p>Capable of handling markdown editing.</p>
          </li>
          <li>
            <p>Contains a modular library to load the necessary functionality on demand.</p>
          </li>
          <li>
            <p>Provides a fully customizable toolbar.</p>
          </li>
          <li>
            <p>Provides HTML view to edit the source directly for developers.</p>
          </li>
          <li>
            <p>Supports third-party library integration.</p>
          </li>
          <li>
            <p>Allows preview of modified content before saving it.</p>
          </li>
          <li>
            <p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p>
          </li>
          <li>
            <p>Contains undo/redo manager.</p>
          </li>
          <li>
            <p>Creates bulleted and numbered lists.</p>
          </li>
        </ul>
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}

## Image delete

To remove an image from the Rich Text Editor content, select the image and click **Remove** tool from the quick toolbar. It will delete the image from the RTE content as well as from the service location if the saveUrl is given.

Once you select the image from the local machine, the URL for the image will be generate. From there, you can remove the image from the service location by clicking the cross icon.

![RTE Image delete](images/image-del.png)

The following sample explains, how to configure `removeUrl` to remove a saved image from the remote service location, when the following image remove actions are performed:

* `delete` key action.
* `backspace` key action.
* Removing uploaded image file from the insert image dialog.
* Deleting image using the quick toolbar `remove` option.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - RemoveUrl Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  private toolbarSettings: object = {
    items: ['Image']
  }

  private insertImageSettings: object = {
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
  }

  public render() {
    return (
      <RichTextEditorComponent height={450} toolbarSettings={this.toolbarSettings} insertImageSettings={insertImageSettings}>
        <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
          Users can format their content using standard toolbar commands.</p>
        <p><b>Key features:</b></p>
        <ul>
          <li>
            <p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p>
          </li>
          <li>
            <p>Capable of handling markdown editing.</p>
          </li>
          <li>
            <p>Contains a modular library to load the necessary functionality on demand.</p>
          </li>
          <li>
            <p>Provides a fully customizable toolbar.</p>
          </li>
          <li>
            <p>Provides HTML view to edit the source directly for developers.</p>
          </li>
          <li>
            <p>Supports third-party library integration.</p>
          </li>
          <li>
            <p>Allows preview of modified content before saving it.</p>
          </li>
          <li>
            <p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p>
          </li>
          <li>
            <p>Contains undo/redo manager.</p>
          </li>
          <li>
            <p>Creates bulleted and numbered lists.</p>
          </li>
        </ul>
        <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
      </RichTextEditorComponent>
    );
  }
}

export default App;

```

{% endtab %}

## Insert from web

To insert an image from the online source like Google, Ping, etc., you should enable the image tool on the editor’s toolbar. By default, the image tool opens a simple dialog which allows you to insert an image from online source.

![RTE Image insert](images/image-web.png)

## Dimension

Sets the default width and height of the image when it is inserted in the Rich Text Editor using [width](/rich-text-editor/api-imageSettingsModel.html#width) and [height](/rich-text-editor/api-imageSettingsModel.html#height)  of the insertImageSettings.
Through the quick toolbar, change the width and height using `Change Size` option. Once you click, the Image Size dialog box will open as follows. In that, you can specify the width and height of the image in pixel.

![RTE Image dimension](images/image-size.png)

## Caption and Alt Text

Image caption and alternative text can be specified for the inserted image in the Rich Text Editor through the quick toolbar options such as, Image Caption and Alternative Text.

Through the Alternative Text option, set the alternative text for the image, when the image is not upload successfully into the Rich Text Editor.

By clicking the Image Caption, the image will get wrapped in an image element with a caption. Then, you can type caption content inside the Rich Text Editor.

## Display position

Sets the default display for an image when it is inserted in the Rich Text Editor using [display](/rich-text-editor/api-imageSettingsModel.html#display) field in [insertImageSettings](/rich-text-editor/api-imageSettingsModel.html). It has two possible options: 'inline' and 'block'.

```typescript
let defaultRTE: RichTextEditor = new RichTextEditor({
    insertImageSettings: {
      display: 'inline'
    }
});
defaultRTE.appendTo('#defaultRTE');
```

## Image with link

The hyperlink itself can be an image in Rich Text Editor. If the image given as hyperlink, the remove, edit, and open link will be added to the quick toolbar of image. For further details about link, see the [link](/rich-text-editor/link.html) documentation.

![RTE image with link](images/image-link.png)

## Resize

Rich Text Editor has a built-in image inserting support.  The resize points will be appearing on each corner of image when focus. So, users can resize the image using mouse points or thumb through the resize points easily. Also, the resize calculation will be done based on aspect ratio.

![RTE image resize](images/image-resize.png)

## Drag and Drop

By default, the Rich Text Editor allows you to insert images by drag-and-drop from the local file system such as Windows Explorer into the content editor area. And, you can upload the images to the server before inserting into the editor by configuring the saveUrl property. The images can be repositioned anywhere within the editor area by dragging and dropping the image.

In the following sample, you can see feature demo.

{% tab template="rich-text-editor/drag-drop", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript
/**
 * Initilaize Rich Text Editor from React element
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public insertImageSettings: object = {
            saveUrl : 'https://aspnetmvc.syncfusion.com/services/api/uploadbox/Save'
        };
  public render() {
    return (
          <RichTextEditorComponent  insertImageSettings={this.insertImageSettings}>
              <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content. Users can format their content using standard toolbar commands.</p>

              <p><b>Key features:</b></p>
              <ul>
                  <li>
                      <p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p>
                  </li>
                  <li>
                      <p>Capable of handling markdown editing.</p>
                  </li>
                  <li>
                      <p>Contains a modular library to load the necessary functionality on demand.</p>
                  </li>
                  <li>
                      <p>Provides a fully customizable toolbar.</p>
                  </li>
                  <li>
                      <p>Provides HTML view to edit the source directly for developers.</p>
                  </li>
                  <li>
                      <p>Supports third-party library integration.</p>
                  </li>
                  <li>
                      <p>Allows preview of modified content before saving it.</p>
                  </li>
                  <li>
                      <p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p>
                  </li>
                  <li>
                      <p>Contains undo/redo manager.</p>
                  </li>
                  <li>
                      <p>Creates bulleted and numbered lists.</p>
                  </li>
              </ul>
              <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar]} />
          </RichTextEditorComponent>
    );
  }
}

export default App;
```

{% endtab %}

### Drag and drop with specific extension images

You can allow the specific images alone to be uploaded using the the allowedTypes property. By default, the Rich Text Editor allows the JPG, JPEG, and PNG formats. You can configure this formats as follows.

``` typescript
    insertImageSettings: {
      allowedTypes: ['.jpg']
    }

```

### Prevent drag and drop action

You can prevent drag-and-drop action by setting the actionBegin argument cancel value to true. The following code shows how to prevent the drag-and-drop.

``` typescript
    actionBegin: function (args: any): void {
        if(args.type === 'drop' || args.type === 'dragstart') {
            args.cancel =true;
        }
    }

```

{% endtab %}