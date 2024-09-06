# Range

Range represents the entire span of the progress bar and can be defined using the `minimum` and `maximum` properties. The default value of the range is 0 to 100.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="Circular"
                        type='Circular'
                        height='160px'
                        trackThickness={24}
                        progressThickness={24}
                        minimum={0}
                        maximum={1}
                        value={0.5}
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}
    >
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}