---
title: "Delete a specific annotation using deleteAnnotationById"
component: "PDF Viewer"
description: "Learn how to delete a specific annotation using deleteAnnotationById in PDF Viewer control."
---

# Delete a specific annotation using deleteAnnotationById

The PDF Viewer library allows you to delete a specific annotation from a PDF document. Deleting a specific annotation can be done using the **deleteAnnotationById()** method. This method is used to delete a specific annotation using its id.

The following steps are used to delete a specific annotation from PDF Document.

**Step 1:** Follow the steps provided in the [link](https://ej2.syncfusion.com/angular/documentation/pdfviewer/getting-started/) to create a simple PDF Viewer sample.

**Step 2:** Use the following code snippet to delete a specific annotation using `deleteAnnotationById()` method.

```html
<button onclick="deleteAnnotationbyId()">Delete Annotation by ID</button>

<script>
  // Delete Annotation by id.
  function deleteAnnotationbyId() {
  var viewer = document.getElementById('container').ej2_instances[0];
  viewer.annotationModule.deleteAnnotationById(viewer.annotationCollection[0].annotationId);
  }
</script>
```

Find the sample, [how to delete a specific annotation using deleteAnnotationById](https://stackblitz.com/edit/react-6bwfsn-ckeqja?file=index.html)