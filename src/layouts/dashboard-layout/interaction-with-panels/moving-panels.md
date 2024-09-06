---
title: "Moving of panels programmatically"
component: "Dashboard Layout"
description: "This section explains how to move the panels programmatically within the layout in Essential JS 2 Dashboard Layout component"
---

# Moving of panels programmatically

Other than drag and drop, it is possible to move the panels in Dashboard Layout programmatically. This can be achieved using [movePanel](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#movepanel) method. The method is invoked as follows,

```js
movePanel(id, row, col)

```

Where,
* id - ID of the panel which needs to be moved.
* row - New row position for moving the panel.
* col - New column position for moving the panel.

Each time a panel's position is changed(Programmatically or through UI interaction), the Dashboard Layout's [change](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#change) event will be triggered.

The following sample demonstrates moving a panel programmatically to a new position in the Dashboard Layout's [created](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#created) event.

{% tab template="dashboard-layout/moving",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css" %}

{% endtab %}