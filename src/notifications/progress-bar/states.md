# Modes

Visualize progress in different modes.

## Determinate

<!-- markdownlint-disable MD033 -->

This is the default state. You can use it when the progress estimation is known.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ProgressBarComponent } from "@syncfusion/ej2-react-progressbar";
ReactDOM.render(
        <ProgressBarComponent
          id="linear"
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

## Indeterminate

By enabling the **IsIndeterminate** property, the state of the progress bar can be changed to indeterminate when the progress cannot be estimated or is not being calculated. It can be combined with determinate mode to know that the application is estimating progress before the actual progress starts.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ProgressBarComponent } from "@syncfusion/ej2-react-progressbar";
ReactDOM.render(
        <ProgressBarComponent
          id="linear"
          type="Linear"
          height="60"
          value={20}
          isIndeterminate={true}
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

## Buffer

<!-- markdownlint-disable MD033 -->
You can use a secondary progress indicator when the primary progress depends on the secondary progress. This will allow users to visualize both primary and secondary progress simultaneously.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ProgressBarComponent } from "@syncfusion/ej2-react-progressbar";
ReactDOM.render(
        <ProgressBarComponent
          id="linear"
          type="Linear"
          height="60"
          value={40}
          secondaryProgress={60}
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