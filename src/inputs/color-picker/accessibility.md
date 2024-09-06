---
title: "ColorPicker Accessibility"
component: "ColorPicker"
description: "The ColorPicker control has accessibility support to access the features via keyboard, screen readers, or other assistive technology devices."
---

# Accessibility

## ARIA attributes

The web accessibility makes web content and web applications more accessible for people with disabilities. It especially helps in dynamic content change and development of advanced user interface controls with AJAX, HTML, JavaScript, and related technologies. It helps to provide information about the widget for assistive technology to the disabled person in screen reader.

ColorPicker provides built-in compliance with the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices) specifications. WAI-ARIA supports is achieved through the attributes like `aria-label`and `aria-selected` applied to the color palette tiles.

To know about the accessibility of SplitButton, refer to the SplitButton [`Accessibility`](./../split-button/accessibility#accessibility) section.

| Properties | Functionality |
| ------------ | ----------------------- |
| role | Specified as `gridcell` for the tiles in the color palette. |
| aria-label | Holds the color of the tile. |
| aria-selected | Indicates the current selected state of the tile. |

## Keyboard interaction

To know about the keyboard interaction of SplitButton, refer to the SplitButton [`Keyboard interaction`](./../split-button/accessibility#keyboard-interaction) section.

The following list of keys can be used to interact with the ColorPicker after the popup has opened.

| **Press** | **To do this** |
| --- | --- |
| <kbd>Upper Arrow</kbd>  | Moves the handler/tile up from the current position. |
| <kbd>Down Arrow</kbd>  | Moves the handler/tile down from the current position. |
| <kbd>Left Arrow</kbd>  | Moves the handler/tile left from the current position. |
| <kbd>Right Arrow</kbd>  | Moves the handler/tile right from the current position. |
| <kbd>Enter</kbd>  | Apply the selected color value. |
| <kbd>Tab</kbd>  | To focus the next focusable element in the ColorPicker popup. |

{% tab template="colorpicker/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
   public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent/>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}