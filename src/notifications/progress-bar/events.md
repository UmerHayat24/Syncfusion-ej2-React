# Events

## valueChanged

This event is triggered when the progress value is changed.

{% tab template="progress-bar/events", sourceFiles="app/**/*.tsx" %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import {IProgressValueEventArgs} from '@syncfusion/ej2-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";
let progressInstance: ProgressBarComponent;
  function changeValue() {
    progressInstance.value = 80;
  }
ReactDOM.render(
  <div>
    <button onClick={changeValue}>Change value</button>
    <br></br>
   <ProgressBarComponent id="linear"
                        ref={linear1 => progressInstance = linear1}
                        type='Linear'
                        trackColor='gray'
                        progressColor='blue'
                        value={100}
                        animation={{
                            enable: false,
                            duration: 2000,
                            delay: 0,
                        }}
                        valueChanged={(args: IProgressValueEventArgs) => {
                          args.progressValue = 90;
                        }}
    >
    </ProgressBarComponent>
    </div>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

## progressCompleted

This event is triggered when the progress attains the `maximum` value.

{% tab template="progress-bar/events", sourceFiles="app/**/*.tsx" %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import {IProgressValueEventArgs} from '@syncfusion/ej2-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="linear2"
                        type='Linear'
                        value={100}
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}
                        progressCompleted={(args: IProgressValueEventArgs) => {
                          args.value = 50;
                        }}
    >
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}