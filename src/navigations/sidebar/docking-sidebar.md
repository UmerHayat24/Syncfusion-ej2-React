---
title: "Docking Sidebar"
component: "Sidebar"
description: "Docking lets the sidebar occupy a small vertical area in a page always and typically contains shortened view of navigation options."
---

# Dock

Dock state of the Sidebar reserves some space on the page that always remains in a visible state when the Sidebar is collapsed. It is used to show the short term of a content like icons alone instead of lengthy text. To achieve this , set [`enableDock`](../api/sidebar#enabledock) as true along with required [`dockSize`](../api/sidebar#docksize).

In the following sample, the list item has icon with text representation. On dock state, only icons in list will be visible to represent the hint of the hidden text content.

{% tab template="sidebar/dock", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,style.css" %}

{% endtab %}

## See Also

* [How to add sidebar navigation](./how-to/sidebar-with-treeview)