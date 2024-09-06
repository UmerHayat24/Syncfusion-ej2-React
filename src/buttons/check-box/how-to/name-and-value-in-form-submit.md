---
title: "Name and Value in form submit"
component: "CheckBox"
description: "React CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Name and Value in form submit

The [`name`](../../api/check-box/#name) attribute of the CheckBox is used to group Checkboxes. When the Checkboxes are grouped in form, the checked items [`value`](../../api/check-box/#value) attribute
will post to the server on form submit which can be retrieved through the name. The disabled and unchecked CheckBox
value will not be sent to the server on form submit.

In the following code snippet, Cricket and Hockey are in the checked state, Tennis is in [`disabled`](../../api/check-box/#disabled) state and Basketball is in unchecked state.
Now, the value that is in checked state only be sent on form submit.

{% tab template="check-box/form", sourceFiles="app/**/*.tsx,index.html,index.css, isDefaultActive=true", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent, CheckBoxComponent} from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// Name and Value attribute in form submit.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <form>
        <ul>
            <li><CheckBoxComponent name="Sport" value="Cricket" label="Cricket" checked={true} /></li>

            <li><CheckBoxComponent name="Sport" value="Hockey" label="Hockey" checked={true} /></li>

            <li><CheckBoxComponent name="Sport" value="Tennis" label="Tennis" disabled={true} /></li>

            <li><CheckBoxComponent name="Sport" value="Basketball" label="Basketball" /></li>

            <li><ButtonComponent isPrimary={true}>Submit</ButtonComponent></li>
        </ul>
      </form>
    );
  }
}
ReactDom.render(<App />, document.getElementById('check-box'));
```

{% endtab %}