# Customization

## Segments

We can divide a progress bar into multiple segments using a `segmentCount` to visualize the progress of multiple sequential tasks.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="circular"
                        type='Circular'
                        height='160px'
                        segmentCount={8}
                        value={100}
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

## Thickness

You can customize the thickness of the track  using `trackThickness` and progress using `progressThickness` to render the ProgressBar with different appearances.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="circular"
                        type='Circular'
                        height='160px'
                        width='90%'
                        trackThickness={24}
                        progressThickness={24}
                        value={100}
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

## Radius

The  radius of the progress bar can be customized using `radius` property and  corner can be customized by **cornerRadius** property.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="circular"
                        type='Circular'
                        height='160px'
                        width='90%'
                        trackThickness={80}
                        progressThickness={10}
                        value={100}
                        enableRtl={false}
                        trackColor="#FFD939"
                        radius="100%"
                        progressColor="white"
                        cornerRadius="Round"
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

## InnerRadius

The inner radius of the progress bar can be customized using `innerRadius` property.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="circular"
                        type='Circular'
                        height='160px'
                        width='90%'
                        trackThickness={80}
                        progressThickness={10}
                        value={100}
                        enableRtl={false}
                        trackColor="#FFD939"
                        radius="100%"
                        innerRadius='80%'
                        progressColor="white"
                        cornerRadius="Round"
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

## Progress color and track color

We can customize the color of progress and track by using  **progressColor** and **trackColor** property.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="circular"
                        type='Circular'
                        height='160px'
                        width='90%'
                        trackThickness={24}
                        progressThickness={24}
                        value={50}
                        enableRtl={false}
                        showProgressValue={true}
                        trackColor="#F8C7D8"
                        radius="100%"
                        progressColor="#E3165B"
                        cornerRadius="Round"
                        animation={{
                            enable: true,
                            duration: 2000,
                            delay: 0,
                        }}>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}