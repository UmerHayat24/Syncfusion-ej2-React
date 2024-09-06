---
title: "ButtonGroup Accessibility"
component: "ButtonGroup"
description: "ButtonGroup component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

The web accessibility makes web content and web applications more accessible for people with disabilities. It especially helps in dynamic content change and development of advanced user interface controls with AJAX, HTML, JavaScript, and related technologies.
ButtonGroup provides built-in compliance with `WAI-ARIA` specifications. It helps the people with disabilities by providing information about the widget for assistive
technology in the screen readers. ButtonGroup component contains the `group` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| role | Indicates the `group` for the container that holds two or more buttons. |

## Keyboard interaction

### Normal behavior

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Keyboard shortcuts</b></td>
<td><b>Actions</b></td>
</tr>
<tr>
<td><kbd>Tab</kbd></td>
<td>Focuses the next button in the ButtonGroup.</td>
</tr>
<tr>
<td><kbd>Enter/Space</kbd></td>
<td>Activates the focused button in the ButtonGroup.</td>
</tr>
</table>

### Checkbox behavior

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Keyboard shortcuts</b></td>
<td><b>Actions</b></td>
</tr>
<tr>
<td><kbd>Tab</kbd></td>
<td>Focuses the next button in the ButtonGroup.</td>
</tr>
<tr>
<td><kbd>Space</kbd></td>
<td>Activates the focused button in the ButtonGroup.</td>
</tr>
</table>

### Radiobutton behavior

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Keyboard shortcuts</b></td>
<td><b>Actions</b></td>
</tr>
<tr>
<td><kbd>Tab</kbd></td>
<td>Focuses the active button in the ButtonGroup.</td>
</tr>
<tr>
<td><kbd>Arrow Keys</kbd></td>
<td>Activates next/previous button in the ButtonGroup.</td>
</tr>
</table>

{% tab template="button-group/util", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render ButtonGroup.
class App extends React.Component<{}, {}> {
  public render() {
    return (
      <div>
        <h5>Normal behavior</h5>
        <div className='e-btn-group' role='group'>
          <ButtonComponent>HTML</ButtonComponent>
          <ButtonComponent>CSS</ButtonComponent>
          <ButtonComponent>Javascript</ButtonComponent>
        </div>
        <h5>Checkbox type behavior</h5>
        <div className='e-btn-group' role='group'>
            <input type="checkbox" id="checkbold" name="font" value='bold' />
            <label className="e-btn" htmlFor="checkbold">Bold</label>
            <input type="checkbox" id="checkitalic" name="font" value='italic' />
            <label className="e-btn" htmlFor="checkitalic">Italic</label>
            <input type="checkbox" id="checkunderline" name="font" value='underline' />
            <label className="e-btn" htmlFor="checkunderline">Underline</label>
        </div>
        <h5>Radiobutton type behavior</h5>
        <div className='e-btn-group' role='group'>
            <input type="radio" id="radioleft" name="align" value='left'/>
            <label className="e-btn" htmlFor="radioleft">Left</label>
            <input type="radio" id="radiomiddle" name="align" value='middle'/>
            <label className="e-btn" htmlFor="radiomiddle">Center</label>
            <input type="radio" id="radioright" name="align" value='right'/>
            <label className="e-btn" htmlFor="radioright">Right</label>
        </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('buttongroup'));

```

{% endtab %}