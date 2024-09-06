# How to add custom menu item in context menu

The context menu can be customized using the [contextMenuSettings](../../api/file-manager/#contextmenusettings), [menuOpen](../../api/file-manager/#menuopen), and [menuClick](../../api/file-manager/#menuclick) events.

The following example shows adding a custom item in the context menu.

The [contextMenuSettings](../../api/file-manager/#contextmenusettings) is used to add new menu item. The [menuOpen](../../api/file-manager/#menuopen) event is used to add the icon to the new menu item. The [menuClick](../../api/file-manager/#menuclick) event is used to add an event handler to the new menu item.

{% tab template="file-manager/contextmenu", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}