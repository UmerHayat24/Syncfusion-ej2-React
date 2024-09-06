---
title: "Localization"
component: "Uploader"
description: "Explains how to localize (locale) all the static text of the file upload control using L10n library that helps to adapt with different cultures."
---

# Localization

The Localization library allows you to localize static text content of the uploader.
The static text contains default text content of action buttons, file status, clear icon title, tooltips,
and text content of drag area. Define the locale object for a culture and assign it to L10n load method.

The following list of keys and its values which are used in the uploader component:

| Key | Description |
|------------------------|---------|
| Browse | To customize the browse button text.|
| Clear | To customize the clear button text.|
| Upload | To customize the upload button text. |
| dropFilesHint | To customize the drop area text. |
| uploadFailedMessage | To customize the status text when  the file is failed to upload.|
| uploadSuccessMessage | To customize the status text when  the file is uploaded successfully.|
| removedSuccessMessage | To customize the status text when  the file is removed the successfully from the serve.|
| removedFailedMessage | To customize the status text while the file is failed to remove.|
| inProgress | To customize the status text while the upload is in progress.|
| pauseUpload | To customize the status text while the uploading is paused.|
| fileUploadCancel | To customize the status text when uploading is cancelled.|
| readyToUploadMessage | To customize the status text when the file is selected and ready to upload.|
| invalidMaxFileSize | To customize the status text when the file size is greater than the maximum file size.|
| invalidFileType | To customize the status text when the file type is invalid.|
| invalidMinFileSize | To customize the status text when the file size is less than the minimum file size. |
| remove | To customize tooltip text for remove icon. |
| cancel | To customize tooltip text for cancel icon. |
| delete | To customize tooltip text for delete icon. |

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { L10n } from '@syncfusion/ej2-base';
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public uploadObj: UploaderComponent;
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public componentWillMount(): void {
    L10n.load({
        "fr-CH": {
            "uploader": {
                "Browse"  : "Feuilleter",
                "Clear" : "Clair",
                "Upload" : "Télécharger",
                "cancel": "Annuler",
                "delete": "Supprimer le fichier",
                "dropFilesHint" : "ou Déposer des fichiers ici",
                "inProgress": "Téléchargement",
                "invalidFileType" : "Le type de fichier n'est pas autorisé",
                "invalidMaxFileSize" : "La taille du fichier dépasse 28 Mo",
                "invalidMinFileSize" : "La taille du fichier est trop petite! S'il vous plaît télécharger des fichiers avec une taille minimale de 10 Ko",
                "readyToUploadMessage": "Prêt à télécharger",
                "remove": "Retirer",
                "removedFailedMessage": "Le fichier n'a pas pu être supprimé",
                "removedSuccessMessage": "Fichier supprimé avec succès",
                "uploadFailedMessage" : "Impossible d'importer le fichier",
                "uploadSuccessMessage" : "Fichier téléchargé avec succès",
            }
        }
    })
}

    public render(): JSX.Element {
        return (
            <UploaderComponent asyncSettings = {this.path} locale = 'fr-CH'/>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
