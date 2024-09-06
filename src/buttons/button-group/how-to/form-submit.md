---
title: "Form submit"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Form submit

The name attribute of the input element is used to group the radio/checkbox type ButtonGroup. When the radio/checkbox type are grouped
in the form, the checked items value attribute will be posted to the server on form submit that can be retrieved through the name.
The disabled radio/checkbox type value will not be sent to the server on form submit.

In the following code snippet, the radio type ButtonGroup is explained with male value as checked.
Now, the value that is in checked state will be sent on form submit.

{% tab template="button-group/form", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ButtonGroup in form.
class App extends React.Component<{}, {}> {
  public componentDidMount(): void {
    (document.getElementById('female') as HTMLInputElement).checked = true;
  }
  public render() {
    return (
      <div>
        <form>
          <div className='e-btn-group'>
            <input type="radio" id="male" name="gender" value="male"/>
            <label className="e-btn" htmlFor="male">Male</label>
            <input type="radio" id="female" name="gender" value="female"/>
            <label className="e-btn" htmlFor="female">Female</label>
            <input type="radio" id="transgender" name="gender" value="transgender"/>
            <label className="e-btn" htmlFor="transgender">Transgender</label>
          </div>
          <ButtonComponent isPrimary={true}>Submit</ButtonComponent>
        </form>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}