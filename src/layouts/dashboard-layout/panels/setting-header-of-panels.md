---
title: "Header and Content of Panels"
component: "Dashboard Layout"
description: "This section explains how to add header for the panels in Essential JS 2 DashboardLayout component"
---

# Header and content of panels

The dashboard layout component is mostly used to represent the data used for monitoring or managing a process. These data or any HTML template can be placed as the content of a panel using the `content` property. Also, word or phrase that summarize the panel’s content can be added as the header on the top of each panel using the `header` property of the panel.

The following sample demonstrates how to add content for each panel using the header and content properties of the panels.

{% tab template="dashboard-layout/header",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css" %}

{% endtab %}

# Placing components as content of panels

In a dashboard, components like the chart, grids, maps, gauge, and more can be used to present a complex data. Such components can be placed as the panel content by assigning the corresponding component element as the `content` of the panel.

The following sample demonstrates how to add EJ2 Chart components as the `content` for each panel in the dashboard layout component.

{% tab template="dashboard-layout/header-content",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css"  %}

{% endtab %}
