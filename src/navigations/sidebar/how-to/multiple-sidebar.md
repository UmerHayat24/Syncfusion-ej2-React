---
title: "How To"
component: "Sidebar"
description: "Miscellaneous aspects of customizing the sidebar"
---

# Multiple Sidebar

Two Sidebars can be initialized in a web page with same main content. Sidebars can be initialized
on right side or left side of the main content using [position](../../api/sidebar#position) property.

>The HTML element with class name `e-main-content` will be considered as the main content and both the
Sidebars will behave as side content to this main content area.

{% tab template="sidebar/multiple", compileJsx=true, sourceFiles="app/App.tsx,style.css" %}

{% endtab %}
