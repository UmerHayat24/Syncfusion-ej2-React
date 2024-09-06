# Animation

Progress Bar support to animate the progress by using `animation` property. Enable the animation by setting **enable** property and also you can control the speed by using **duration** property.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="linear"
                        type='Linear'
                        trackThickness={24}
                        progressThickness={24}
                        value={60}
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