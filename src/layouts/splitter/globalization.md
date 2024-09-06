---
title: "Globalization"
component: "Splitter"
description: "This section explains the globalization support of Syncfusion Splitter component."
---

# Globalization

## RTL

Specifies the direction of the Splitter component using the enableRtl property. For writing systems that require it like Arabic, Hebrew, etc., the direction can be switched to right-to-left.

The following code shows how to enable RTL behavior.

{% tab template="splitter/rtl", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public render() {
  return (<div className="App">
    <SplitterComponent id="rtl" height="250px" enableRtl="true">
    <PanesDirective>
      <PaneDirective size='200px' content = 'Left pane'/>
      <PaneDirective size='200px' content = 'Middle pane'/>
      <PaneDirective size='200px' content = 'Right pane'/>
    </PanesDirective>
    </SplitterComponent>
</div>);
}
}
export default App;
```

{% endtab %}

## See Also

* [Migration from Essential JS 1](./ej1-api-migration)