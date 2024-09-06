# Types

Visualize progress in different shapes (rectangle, circle, and semi-circle) to give a unique appearance to your app design.

## Linear

Set **type** to Linear to get the linear progress bar. It also support secondary progress and different mode of progress.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ProgressBarComponent } from "@syncfusion/ej2-react-progressbar";
ReactDOM.render(
                <ProgressBarComponent
                  id="lineardeterminate"
                  type="Linear"
                  height="60"
                  value={100}
                  animation={{
                    enable: true,
                    duration: 2000,
                    delay: 0
                  }}
                >
                </ProgressBarComponent>,
          document.getElementById("container") as HTMLElement
    );
```

{% endtab %}

## Circular

Set **type** to Circular to get the circular progress bar. It also support secondary progress and different mode of progress.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ProgressBarComponent } from "@syncfusion/ej2-react-progressbar";
ReactDOM.render(
                <ProgressBarComponent
                  id="circular-container"
                  type="Circular"
                  height="160px"
                  value={100}
                  animation={{
                    enable: true,
                    duration: 2000,
                    delay: 0
                  }}
                >
                </ProgressBarComponent>,
      document.getElementById("container") as HTMLElement
    );
```

{% endtab %}