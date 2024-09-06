---
title: "Rich Text Editor Form Support"
component: "Rich Text Editor"
description: "This section for Syncfusion react Rich Text Editor component demonstrates that how to work with form and it's validation."
---

# Form support

The following sample demonstrates how to get the Rich Text Editor value in button click.

Render the Rich Text Editor in form.

```typescript
  <form id="myForm" class="form-vertical">
    <div class="form-group">
      <textarea id="defaultRTE" name="defaultRTE" required maxlength="100" minlength="20" data-msg-containerid="dateError"></textarea>
      <div id="dateError"></div>
    </div>
    <div class="form-btn-section">
      <button id="validateSubmit" class="sample-btn e-control e-btn" type="submit" data-ripple="true">Submit</button>
      <button id="resetbtn" class="sample-btn e-control e-btn" type="reset" data-ripple="true">Reset</button>
    </div>
  </form>
```

Upon submitting the form, the getValue method will be triggered. Through the FormData class, get the Rich Text Editor value.

{% tab template="rich-text-editor/form", sourceFiles="app/App.tsx", isDefaultActive = "true", compileJsx=true %}

```typescript

/**
 * Rich Text Editor - Form Sample
 */
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { Count, HtmlEditor, Image, Inject, Link, QuickToolbar, RichTextEditorComponent, Toolbar } from '@syncfusion/ej2-react-richtexteditor';
// import * as Marked from 'marked';
import * as React from 'react';

class App extends React.Component<{},{}> {
  public formObject: FormValidatorModel;
  public componentDidMount(): void {
    const option: FormValidatorModel = {
      rules: {
        defaultRTE: {
          maxLength:[108, 'Maximum 100 character only'],
          minLength: [15, 'Need atleast 8 character length'],
          required: true,
        }
      }
    };
    this.formObject = new FormValidator('#myForm', option);
    (document as any).getElementById('validateSubmit').addEventListener('click', (e: any) => {
      const form = (document.forms as any).myForm;
      const formData = new FormData(form);
      const rteValue = formData.get('defaultRTE');
      // Use this value to the data base.
      alert(rteValue);
      e.preventDefault();
    });
  }

  public render() {
    return (
      <form id="myForm" className="form-vertical">
        <div className="form-group">
          <RichTextEditorComponent id="defaultRTE" name="defaultRTE" className="form-control" height={200} showCharCount={true} maxLength={100} placeholder={'Type something'} value={''}>
            <Inject services={[Toolbar, Image, Link, HtmlEditor, QuickToolbar, Count]} />
          </RichTextEditorComponent>
        </div>
        <div className="form-btn-section">
          <button id="validateSubmit" className="sample-btn e-control e-btn" type="submit" data-ripple="true">Submit</button>
          <button id="reset-btn" className="sample-btn e-control e-btn" type="reset" data-ripple="true">Reset</button>
        </div>
      </form>
    );
  }
}

export default App;

```

{% endtab %}