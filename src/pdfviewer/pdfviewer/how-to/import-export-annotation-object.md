---
title: "Import and Export annotation as object"
component: "PDF Viewer"
description: "Learn how to import and export annotation as object in PDF Viewer control."
---

# Import and Export annotation as object

The PDF Viewer library allows you to import annotations from objects or streams instead of loading it as a file. To import such annotation objects, the PDF Viewer control must export the PDF annotations as objects using the [**ExportAnnotationsAsObject()**](https://ej2.syncfusion.com/react/documentation/api/pdfviewer/#exportannotationsasobject) method. Only the annotations objects that are exported from the PDF Viewer can be imported.

The following steps are used to import and export annotation as object.

**Step 1:** Follow the steps provided in the [link](https://ej2.syncfusion.com/react/documentation/pdfviewer/getting-started/) to create a simple PDF Viewer sample.

**Step 2:** Use the following code snippet to perform import and export annotation.

```html
<button onclick="exportAnnotation()">Export Annotation</button>
<button onclick="importAnnotation()">Import Annotation</button>

<script>
var exportObject;
// Export annotation as object.
function exportAnnotation(){
    var viewer = document.getElementById('container').ej2_instances[0];
    viewer.exportAnnotationsAsObject().then(function(value) {
    exportObject = value;
    });
}

// Import annotation that are exported as object.
function importAnnotation() {
    var viewer = document.getElementById('container').ej2_instances[0];
    viewer.importAnnotation(JSON.parse(exportObject));
}
</script>
```

Find the Sample, [how to import and export annotation as object](https://stackblitz.com/edit/react-dtuvxn?devtoolsheight=33&file=index.html)