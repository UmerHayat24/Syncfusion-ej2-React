# how to add custom menu item in context menu

The context menu can be customized using the [contextMenuSettings](../../api/file-manager/#contextMenuSettings),[menuOpen](../../api/file-manager/#menuOpen), and [menuClick](../../api/file-manager/#menuClick) events.

The following example shows adding a custom item in the context menu.

The [menuOpen](../../api/file-manager/#menuOpen) event is used to add the new menu item. The [menuClick](../../api/file-manager/#menuClick) event is used to add event handler to the new menu item.

{% tab template="file-manager/contextmenu", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}