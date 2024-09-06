---
title: "Auto Close"
component: "Sidebar"
description: "Sidebar can be initialized in expand or collapsed state in user specified resolutions."
---

# Auto-close

Sidebar often behaves differently on mobile display and differently on desktop display. It has an effective feature that offers
to set it in opened or closed state depending on the specified resolution. This is achieved
through [mediaQuery](../api/sidebar#mediaquery) property that allows you to set the Sidebar in an expanded state or collapsed state only in user-defined resolution.

{% tab template="sidebar/auto-close-max", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,style.css" %}

{% endtab %}

* In this sample,the Sidebar will be in expanded state only in resolution below `400px`.

{% tab template="sidebar/auto-close-min", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html,style.css" %}

```typescript

```

{% endtab %}