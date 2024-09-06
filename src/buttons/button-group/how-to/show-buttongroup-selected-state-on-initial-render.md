---
title: "Show ButtonGroup selected state on initial render"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Show ButtonGroup selected state on initial render

To show selected state on initial render, `checked` property should to added to the corresponding
input element.

The following example illustrates how to show selected state on initial render.

{% tab template="button-group/default", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render checkbox type ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <div className='e-btn-group'>
            <input type="checkbox" id="checkbold" name="font" value="bold" checked={true}/>
            <label className="e-btn" htmlFor="checkbold">Bold</label>
            <input type="checkbox" id="checkitalic" name="font" value="italic" />
            <label className="e-btn" htmlFor="checkitalic">Italic</label>
            <input type="checkbox" id="checkline" name="font" value="underline"/>
            <label className="e-btn" htmlFor="checkline">Underline</label>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}