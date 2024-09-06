---
title: Responsive Dashboard"
component: "Dashboard Layout"
description: "This section explains about responsiveness and adaptivity of Essential JS 2 Dashboard Layout component"
---

# Responsive and adaptive layout

The control is provided with built-in responsive support, where panels within the layout get adjusted based on their parent element's dimensions to accommodate any resolution which relieves the burden of building responsive dashboards.

The dashboard layout is designed to automatically adapt with lower resolutions by transforming the entire layout into a stacked one, so that, the panels will be displayed in a vertical column. By default, whenever the screen resolution meets 600 px or lower resolutions this layout transformation occurs. This transformation can be modified for any user defined resolution by defining the for the `mediaQuery` property of the component.

The following sample demonstrates the usage of the `mediaQuery` property to turn out the layout into a stacked one in user defined resolution. Here, whenever, the window size reaches 700 px or lesser, the layout becomes a stacked layout.

{% tab template="dashboard-layout/responsive-adaptive",compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,App.css" %}

{% endtab %}