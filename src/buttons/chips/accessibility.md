# Accessibility

## Keyboard interaction

The following shortcut keys are used to access the Chip control without any interruption.

| Keyboard shortcuts | Actions |
|------------|-------------------|
| <kbd>Enter</kbd> | Selects the targeted chip from the ChipList/ChipCollection. |
| <kbd>Delete</kbd> | Deletes the targeted chip from the ChipList/ChipCollection. |

{% tab template="chips/avatar", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ChipListComponent, ChipsDirective, ChipDirective } from '@syncfusion/ej2-react-buttons';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

// To render Chip.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <ChipListComponent id="chip-avatar" enableDelete={true}>
            <ChipsDirective>
                <ChipDirective text="Andrew" avatarIconCss="andrew"></ChipDirective>
                <ChipDirective text="Janet" avatarIconCss="janet"></ChipDirective>
                <ChipDirective text="Laura" avatarIconCss="laura"></ChipDirective>
                <ChipDirective text="Margaret" avatarIconCss="margaret"></ChipDirective>
            </ChipsDirective>
        </ChipListComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('chip'));
```

{% endtab %}