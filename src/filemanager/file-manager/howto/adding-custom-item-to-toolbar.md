# How to add custom button in toolbar

The toolbar items can be customized using the [toolbarSettings](../../api/file-manager/#toolbarSettings) API and [toolbarClick](../../api/file-manager/#toolbarClick) event.

The following example shows adding a custom item in the toolbar.

The new toolbar button is added using [toolbarSettings](../../api/file-manager/#toolbarSettings). The [toolbarClick](../../api/file-manager/#toolbarClick) event is used to add an event handler to the new toolbar button.

{% tab template="file-manager/toolbar", compileJsx=true, sourceFiles="app/App.tsx,app/index.tsx,index.html" %}

{% endtab %}