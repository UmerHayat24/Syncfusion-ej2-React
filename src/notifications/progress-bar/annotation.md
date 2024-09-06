# Annotation and Label

## Annotation

In the circular progress bar, you can add any view to the center using the **Content** property in annotation.

For example, you can include add, start, or pause button to control the progress. You can also add an image that indicates the actual task in progress or add custom text that conveys how far the task is completed.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent, ProgressBarAnnotationsDirective, ProgressBarAnnotationDirective, Inject,
    ProgressAnnotation } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";
let content: string = '<div id="point1" style="font-size:20px;font-weight:bold;color:#ffffff;fill:#ffffff"><span>60%</span></div>';
ReactDOM.render(
   <ProgressBarComponent id="circular"
                        type='Circular'
                        innerRadius="190%"
                        height='160px'
                        trackThickness={80}
                        cornerRadius={"Round"}
                        trackColor={"#FFD939"}
    >
    <Inject services={[ProgressAnnotation]} />
                                    <ProgressBarAnnotationsDirective>
                                        <ProgressBarAnnotationDirective content={content}>

                                        </ProgressBarAnnotationDirective>
                                    </ProgressBarAnnotationsDirective>
    </ProgressBarComponent>,
  document.getElementById("container") as HTMLElement
);
```

{% endtab %}

## Label

You can show the progress value in both linear and cicular progress bar using **showProgressValue** property.

{% tab template="progress-bar/default", sourceFiles="app/**/*.tsx", isDefaultActive=true %}

```typescript
import { ProgressBarComponent } from '@syncfusion/ej2-react-progressbar';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
   <ProgressBarComponent id="linear"
                        type='Linear'
                        showProgressValue={true}
                        labelStyle={{color: '#FFFFFF'}}
                        trackThickness={24}
                        progressThickness={24}
                        value={50}
                        textRender={(args: ITextRenderEventArgs) => {
                        args.text = '50';
                          }}
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