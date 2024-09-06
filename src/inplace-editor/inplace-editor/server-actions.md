---
title: "Server actions"
component: "In-place Editor"
description: "Learn how to modify and submit a value to the server and handle success and failure events in the Essential JS2 React In-place Editor component."
---

# Server actions

By passing In-place Editor component value to the server, the [primaryKey](../api/inplace-editor/#primarykey) property value must required otherwise action not performed for remote data.

If the [URL](../api/inplace-editor/#url) property value is empty, data passing will handled at local and also the [actionSuccess](../api/inplace-editor/#actionsuccess) event will trigger with `null` as argument value.

> The following arguments are passed to the server when submit actions perform.

| Arguments  | Explanations                                              |
|------------|-----------------------------------------------------------|
| value      | For processing edited value, like DB value updating.      |
| primaryKey | For value mapping to the server, like selecting DB.            |
| name       | For field mapping to the server, like DB column field mapping. |

Find the following sample server codes for defining models and controller functions to configure processing data.

```C#
  public class SubmitModel {
      public string Name { get; set; }
      public string PrimaryKey { get; set; }
      public string Value { get; set; }
  }
```

```C#

public IEnumerable<SubmitModel> UpdateData([FromBody]SubmitModel value) {
  // User can process data
  return value;
}

```

* When Server actions successfully done, the [actionSuccess](../api/inplace-editor/#actionsuccess) event will be fired with returned server data.

* If the server is not responding, the [actionFailure](../api/inplace-editor/#actionfailure) event will be fired with data, but value not updated in the Editor.

In the following sample, the `actionSuccess` event will trigger once the value submitted successfully into the server. In this sample, both `actionSuccess` and `actionFailure` were configured and resulted value will be converted to chips.

{% tab template="in-place-editor/server-actions", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ActionEventArgs, Inject, InPlaceEditorComponent, MultiSelect } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public inplaceEditorObj: InPlaceEditorComponent;
  
  public serviceUrl = 'https://ej2services.syncfusion.com/development/web-services/api/Editor/UpdateData';
  public frameWorkList = ['Android', 'JavaScript', 'jQuery', 'TypeScript', 'Angular', 'React', 'Vue', 'Ionic'];
  public value = ['JavaScript', 'jQuery'];
  public model = { mode: 'Box', dataSource: this.frameWorkList, placeholder: 'Select skill' };

  public chipOnCreate(): void {
    (this.inplaceEditorObj as any).element.querySelector('.e-editable-value').innerHTML = this.chipCreation((this.inplaceEditorObj.value as string[]), true);
  }

  public onActionSuccess(e: ActionEventArgs): void {
    e.value = this.chipCreation(e.value.split(','), true);
  }

  public onActionFailure(e: ActionEventArgs): void {
    e.value = this.chipCreation(e.value.split(','), false);
  }

  public chipCreation(data: string[], isSuccess: boolean): string {
    let value: string = '<div class="e-chip-list">';
    [].slice.call(data).forEach((val: string) => {
        value += '<div class="e-chip"> <span class="e-chip-text' + (!isSuccess ? 'e-highlight' : '') + '"> ' + val + '</span></div>';
    });
    value += '</div>';
    return value;
  }

  public create(): void {
    this.chipOnCreate();
  }

  public render() {
    return (
    <div id='container'>
         <span className="content-title"> Select frameworks: </span>
         <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='multiselect' data-underline='false' mode='Inline' type='MultiSelect' value={this.value} name='skill' url={this.serviceUrl} primaryKey='FrameWork' adaptor='UrlAdaptor' model={this.model} actionSuccess={ this.onActionSuccess=this.onActionSuccess.bind(this) } actionFailure={ this.onActionFailure=this.onActionFailure.bind(this) } created={this.create=this.create.bind(this)} >
         <Inject services={[MultiSelect]} />
         </InPlaceEditorComponent>
     </div>
    );
  }
}

export default App;
```

{% endtab %}

## See Also

* [Indicate the server actions in the editor](./how-to/custom-indication/)