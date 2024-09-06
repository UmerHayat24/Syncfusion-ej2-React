---
title: "Custom Context"
component: "Sidebar"
description: "Sidebar can set to be initialized , target to any HTML element alongside of the main content of a web page."
---

# Target

By default, Sidebar initializes target to the body element. Using the [target](../api/sidebar#target) property, set target element
to initialize the Sidebar inside any HTML element apart from the body element.

> If required , `zIndex` can be set when sidebar act as overlay type.

{% tab template="sidebar/contextTo", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,style.css" %}

{% endtab %}