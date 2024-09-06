---
title: "Variatons"
component: "Sidebar"
description: "The different types in type property of the sidebar gives flexibility to view or hide the content (primary/secondary) over/above the main content by pushing, sliding, or overlaying it."
---

# Types

The Sidebar component's expand behavior can be modified based on the purpose of use.

* Expanding types of the Sidebar

## Expanding types of Sidebar

Sidebar can be set to initialize based on four different types that are consistent with the main component as explained below. When `dataBind` is invoked, this applies the pending property changes immediately to the component.

 | Item | Description |
|-----|-----|
| [`Over`](../api/sidebar#type) | Sidebar floats over the main content area.|
| [`Push`](../api/sidebar#type) | Sidebar pushes the main content area to appear side-by-side, and shrinks the main content within the screen width.|
| [`Slide`](../api/sidebar#type) | Sidebar translates the x and y positions of main content area based on the Sidebar width. The main content area will not be adjusted within the screen width. |
| [`Auto`](../api/sidebar#type) | Sidebar with `Over` type in mobile resolution, and `Push` type in other higher resolutions. |

> `Auto` is the default expand mode.

In the following sample, the types of Sidebar are demonstrated.

{% tab template="sidebar/variations", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,style.css" %}

{% endtab %}

## See Also

* [How to add sidebar with custom animation](./how-to/sidebar-with-variation-animation)
* [How to add multiple sidebar](./how-to/multiple-sidebar)