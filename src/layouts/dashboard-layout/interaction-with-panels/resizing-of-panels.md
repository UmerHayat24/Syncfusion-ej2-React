---
title: "Resizing panels"
component: "Dashboard Layout"
description: "This section explains how to enable resizing and the dynamic resizing of panels within the layout in Essential JS 2 DashboardLayout component"
---

# Resizing panels

The Dashboard Layout component is also provided with the panel resizing functionality which can be enabled or disabled using the `allowResizing` property. This functionality allows you to resize the panels dynamically through UI interactions using the resizing handlers which controls the panel resizing in various directions.

Initially, the panels can be resized only in south-east direction. However, panels can also be resized in east, west, north, south and south-west directions by defining the required directions with the `resizableHandles` property.

On resizing a panel in Dashboard layout the following events will be triggered,
* [resizeStart](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#resizestart) - Triggers when panel resize starts
* [resize](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#resize) - Triggers when panel is being resized
* [resizeStop](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#resizestop) - Triggers when panel resize stops

The following sample demonstrates how to enable and disable the resizing of panels in the Dashboard Layout component in different directions.

{% tab template="dashboard-layout/resizing",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css"%}

{% endtab %}

# Resizing panels programmatically

The Dashboard Layout panels can also be resized programmatically by using [resizePanel](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#resizepanel) method. The method is invoked as follows,

```js
resizePanel(id, sizeX, sizeY)

```

Where,
* id - ID of the panel which needs to be resized.
* sizeX - New panel width in cells count for resizing the panel.
* sizeY - New panel height in cells count for resizing the panel.

The following sample demonstrates resizing panels programmatically in the Dashboard Layout's [created](https://ej2.syncfusion.com/react/documentation/api/dashboard-layout/#created) event.

{% tab template="dashboard-layout/resize-programmatically",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css"%}

{% endtab %}