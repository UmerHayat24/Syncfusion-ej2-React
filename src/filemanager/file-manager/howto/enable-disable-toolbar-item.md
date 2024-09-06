# How to enable/disable toolbar item/items

The toolbar items can be enabled/disabled by specifying the items in [enableToolbarItems](../../api/file-manager/#enabletoolbaritems) or [disableToolbarItems](../../api/file-manager/#disabletoolbaritems) methods respectively.

The following example shows enabling and disabling toolbar items on button click.

The new toolbar button is added using [toolbarSettings](../../api/file-manager/#toolbarSettings). The [toolbarClick](../../api/file-manager/#toolbarClick) event is used to add an event handler to the new toolbar button.

{% tab template="file-manager/toolbar-item", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}