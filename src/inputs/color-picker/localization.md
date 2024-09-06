---
title: "ColorPicker Localization"
component: "ColorPicker"
description: "This section helps to learn how to create the color picker in React application with Localiation"
---

# Localization and RTL

## Localization

The `Localization` library allows you to localize default text content of the
ColorPicker. The ColorPicker component has static text for `control buttons (apply / cancel)` and `mode switcher` that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/color-picker#locale) value and translation object.

The following list of properties and its values are used in the ColorPicker.

Locale key words |Text
-----|-----
Apply |Apply
Cancel |Cancel
ModeSwitcher |Switch Mode

### Loading translations

To load translation object in an application use `load` function of `L10n` class.

The below example demonstrates the ColorPicker in `Deutsch` culture.

{% tab template="colorpicker/how-to", isDefaultActive = "true", sourceFiles="app/**/index.tsx", compileJsx=true %}

```tsx
import { L10n } from '@syncfusion/ej2-base';
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

L10n.load({
    'de-DE': {
        'colorpicker': {
            'Apply': 'Anwenden',
            'Cancel': 'Abbrechen',
            'ModeSwitcher': 'Modus wechseln'
        }
    }
});

class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent locale='de-DE'/>
            </div>
          </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Right to Left - RTL

ColorPicker component has `RTL` support. It helps to render the ColorPicker from right-to-left direction.
It improves the user experiences and accessibility for users who use right-to-left languages(Arabic, Farsi, Urdu, etc). This can be achieved by setting the [`enableRtl`](../api/color-picker#enablertl) property to `true`.

The following example illustrates how to enable right-to-left support in ColorPicker component.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { L10n } from '@syncfusion/ej2-base';
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

L10n.load({
    'ar-AE': {
        'colorpicker': {
            'Apply': 'تطبيق',
            'Cancel': 'إلغاء',
            'ModeSwitcher': 'مفتاح كهربائي الوضع'
        }
    }
});

class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent enableRtl={true} locale='ar-AE'/>
            </div>
          </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## See Also

* [More information about localization](./../common/localization)