---
title: "React Rich Text Editor Globalization"
component: "Rich Text Editor"
description: "This section explains the localization support of Syncfusion react Rich Text Editor component."
---

# Globalization

## Localization

The Rich Text Editor provides an option to localize its strings; it is used to adapting the editor to a particular local language. By default, the editor will use the US English (en-US) as its language. Please find the table with a list of keys and their corresponding values for the default language (en-US).

``` javascript
    'en-US': {
      'richtexteditor': {
        align: "Align",
        alignments: "Alignments",
        alttext: "Alternative Text",
        backgroundcolor: "Background color",
        bold: "Bold",
        caption: "Caption",
        clearall: "Clear All",
        clearformat: "Clear Format",
        copy: "Copy",
        createlink: "Insert link",
        cut: "Cut",
        dimension: "Dimension",
        display: "Display",
        editlink: "Edit link",
        fontcolor: "Font Color",
        fontname: "Font Name",
        fontsize: "Font Size",
        formats: "Formats",
        fullscreen: "Full Screen",
        image: "Insert image",
        indent: "Increase Indent",
        insertcode: "Insert Code",
        insertlink: "insertlink",
        italic: "Italic",
        justifycenter: "JustifyCenter",
        justifyfull: "Justify Full",
        justifyleft: "JustifyLeft",
        justifyright: "Justify Right",
        lowercase: "Lower Case",
        maximize: "Maximize",
        minimize: "Minimize",
        openlink: "Open link",
        orderedlist: "ordered list",
        outdent: "Decrease Indent",
        paste: "Paste",
        preview: "Preview",
        print: "Print",
        redo: "Redo",
        remove: "Remove",
        removelink: "remove link",
        replace: "Replace",
        sourcecode: "Source Code",
        strikethrough: "Strikethrough",
        subscript: "Subscript",
        superscript: "Superscript",
        underline: "Underline",
        undo: "Undo",
        unorderedlist: "unordered list",
        uppercase: "Upper Case",
        viewside: "View Side",
        zoomin: "Zoom In",
        zoomout: "Zoom Out",
        formatsDropDownParagraph: "Paragraph",
        formatsDropDownCode: "Code",
        formatsDropDownQuotation: "Quotation",
        formatsDropDownHeading1: "Heading 1",
        formatsDropDownHeading2: "Heading 2",
        formatsDropDownHeading3: "Heading 3",
        formatsDropDownHeading4: "Heading 4",
        fontNameSegoeUI: "Segoe UI",
        fontNameArial: "Arial",
        fontNameGeorgia: "Georgia",
        fontNameImpact: "Impact",
        fontNameTahoma: "Tahoma",
        fontNameTimesNewRoman: "Times New Roman",
        fontNameVerdana: "Verdana"

      }
    }
```

To localize the editor’s strings with your own localization, copy the default language informations and localize the strings in the values column. For example, to localize the editor in German language (“de-DE”).

``` javascript
    'de-DE': {
      'richtexteditor': {
        align: "ausrichten",
        alignments: "Alignments",
        alternateHeader: "Alternatieve tekst",
        alttext: "alternativer Text",
        backgroundColor: "Hintergrundfarbe",
        bold: "fett",
        browse: "Blader",
        caption: "Bildbeschriftung",
        clearAll: "Alles",
        clearFormat: "Klar Format",
        copy: "Kopieren",
        createLink: "Link einfügen",
        cut: "schneiden",
        dialogCancel: "Annuleer",
        dialogInsert: "invoegen",
        dialogUpdate: "Bijwerken",
        dimension: "Größe",
        display: "Anzeige",
        editLink: "Edit link",
        fontColor: "Wählen Sie die Farbe",
        fontName: "Wählen Sie Schriftfamilie",
        fontSize: "Wählen Sie Schriftgröße",
        formats: "Formats",
        fullscreen: "Vollbild",
        image: "Bild einfügen",
        imageAlternateText: "Alternatieve tekst",
        imageCaption: "onderschrift",
        imageDeviceUploadMessage: "Klik hier om te uploaden",
        imageHeader: "Voeg afbeelding in",
        imageHeight: "Hoogte",
        imageLinkHeader: "U kunt ook een link van internet opgeven",
        imageSizeHeader: "Afbeeldingsgrootte",
        imageUploadMessage: "Zet hier een afbeelding neer of klik om te uploaden",
        imageUrl: "URL",
        imageWidth: "Breedte",
        indent: "Einzug",
        insertLink: "Link einfügen",
        insertcode: "Code eingeben",
        italic: "kursiv",
        justifyCenter: "Text-Zentrum",
        justifyFull: "rechtfertigen",
        justifyLeft: "Ausrichten von Text links",
        justifyRight: "Ausrichten von Text rechts",
        linkHeader: "Link invoegen",
        linkOpenInNewWindow: "Open de link in een nieuw venster",
        linkText: "Displaytekst",
        linkTooltipLabel: "tooltip",
        linkWebUrl: "Webadres",
        lowerCase: "Kleinbuchstaben",
        maximize: "Maximieren",
        minimize: "minimieren",
        openLink: "Open link",
        orderedList: "Geordnete Liste einfügen",
        outdent: "Einzug verkleinern",
        paste: "Paste",
        preview: "Vorschau",
        print: "Drucken",
        redo: "Wiederherstellen",
        remove: "Löschen",
        removeLink: "fjern Hyperlink",
        replace: "ersetzen",
        sourcecode: "Quellcode",
        strikethrough: "Durchgestrichen",
        subscript: "index",
        superscript: "Überschrift",
        underline: "unterstreichen",
        undo: "lösen",
        unorderedList: "Legen Sie ungeordnete Liste",
        upperCase: "Großbuchstaben",
        viewside: "Seite anzeigen",
        zoomIn: "hineinzoomen",
        zoomOut: "Rauszoomen",
        formatsDropDownParagraph: "Absatz",
        formatsDropDownCode: "Kodex",
        formatsDropDownQuotation: "Zitat",
        formatsDropDownHeading1: "Überschrift 1",
        formatsDropDownHeading2: "Überschrift 2",
        formatsDropDownHeading3: "Überschrift 3",
        formatsDropDownHeading4: "Überschrift 4",
        fontNameSegoeUI: "Segoe UI",
        fontNameArial: "Arial",
        fontNameGeorgia: "Georgia",
        fontNameImpact: "Einschlag",
        fontNameTahoma: "Tahoma",
        fontNameTimesNewRoman: "Mal Neu römisch",
        fontNameVerdana: "Verdana"

      }
    }
```

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Localization Sample
 */
import { L10n } from '@syncfusion/ej2-base';
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

L10n.load({
  'de-DE': {
    'richtexteditor': {
      align: "ausrichten",
      alignments: "Alignments",
      alternateHeader: "Alternatieve tekst",
      alttext: "alternativer Text",
      backgroundColor: "Hintergrundfarbe",
      bold: "fett",
      browse: "Blader",
      caption: "Bildbeschriftung",
      clearAll: "Alles",
      clearFormat: "Klar Format",
      copy: "Kopieren",
      createLink: "Link einfügen",
      cut: "schneiden",
      dialogCancel: "Annuleer",
      dialogInsert: "invoegen",
      dialogUpdate: "Bijwerken",
      dimension: "Größe",
      display: "Anzeige",
      editLink: "Edit link",
      fontColor: "Wählen Sie die Farbe",
      fontName: "Wählen Sie Schriftfamilie",
      fontSize: "Wählen Sie Schriftgröße",
      formats: "Formats",
      fullscreen: "Vollbild",
      image: "Bild einfügen",
      imageAlternateText: "Alternatieve tekst",
      imageCaption: "onderschrift",
      imageDeviceUploadMessage: "Klik hier om te uploaden",
      imageHeader: "Voeg afbeelding in",
      imageHeight: "Hoogte",
      imageLinkHeader: "U kunt ook een link van internet opgeven",
      imageSizeHeader: "Afbeeldingsgrootte",
      imageUploadMessage: "Zet hier een afbeelding neer of klik om te uploaden",
      imageUrl: "URL",
      imageWidth: "Breedte",
      indent: "Einzug",
      insertLink: "Link einfügen",
      insertcode: "Code eingeben",
      italic: "kursiv",
      justifyCenter: "Text-Zentrum",
      justifyFull: "rechtfertigen",
      justifyLeft: "Ausrichten von Text links",
      justifyRight: "Ausrichten von Text rechts",
      linkHeader: "Link invoegen",
      linkOpenInNewWindow: "Open de link in een nieuw venster",
      linkText: "Displaytekst",
      linkTooltipLabel: "tooltip",
      linkWebUrl: "Webadres",
      lowerCase: "Kleinbuchstaben",
      maximize: "Maximieren",
      minimize: "minimieren",
      openLink: "Open link",
      orderedList: "Geordnete Liste einfügen",
      outdent: "Einzug verkleinern",
      paste: "Paste",
      preview: "Vorschau",
      print: "Drucken",
      redo: "Wiederherstellen",
      remove: "Löschen",
      removeLink: "fjern Hyperlink",
      replace: "ersetzen",
      sourcecode: "Quellcode",
      strikethrough: "Durchgestrichen",
      subscript: "index",
      superscript: "Überschrift",
      underline: "unterstreichen",
      undo: "lösen",
      unorderedList: "Legen Sie ungeordnete Liste",
      upperCase: "Großbuchstaben",
      viewside: "Seite anzeigen",
      zoomIn: "hineinzoomen",
      zoomOut: "Rauszoomen",
      formatsDropDownParagraph: "Absatz",
      formatsDropDownCode: "Kodex",
      formatsDropDownQuotation: "Zitat",
      formatsDropDownHeading1: "Überschrift 1",
      formatsDropDownHeading2: "Überschrift 2",
      formatsDropDownHeading3: "Überschrift 3",
      formatsDropDownHeading4: "Überschrift 4",
      fontNameSegoeUI: "Segoe UI",
      fontNameArial: "Arial",
      fontNameGeorgia: "Georgia",
      fontNameImpact: "Einschlag",
      fontNameTahoma: "Tahoma",
      fontNameTimesNewRoman: "Mal Neu römisch",
      fontNameVerdana: "Verdana"

    }
  }
});

class App extends React.Component<{},{}> {
  public render() {
    return (
      <RichTextEditorComponent  height={450} locale={'de-DE'}>
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

## RTL

Specifies the direction of the Rich Text Editor component using the [enableRtl](../api/rich-text-editor/#enablertl) property. For writing systems that require it like Arabic, Hebrew, etc., the direction can be switched to right-to-left.

**Note:** It will not change based on the locale property.

{% tab template="rich-text-editor/basic", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - RTL Sample
 */
import { HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public render() {
    return (
      <RichTextEditorComponent height={450} enableRtl={true}>
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