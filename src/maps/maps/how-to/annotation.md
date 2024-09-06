# Annotations

Annotations are used to mark the specific area of interest in the Maps with texts, shapes, or images. Any number of annotations can be added to the Maps component.

Initialize the Maps control with annotation option, text content or ID of an HTML element or an HTML string can be specified to render a new element that needs to be displayed in the Maps by using the [`content`](../api/maps/annotationModel/#content) property. To specify the content position with [`x`](../api/maps/annotationModel/#x) and [`y`](../api/maps/annotationModel/#y) properties as mentioned in the following example. In annotation, import the image in the specified Map area by using require function as mentioned in the below example.

```sh
const logo = require('./compass.png');
<img src={logo} height="75px" width="75px"/>
```

[`app.tsx`]

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { africa_continent } from 'africa-continent.ts';
import * as React from 'react';
import { MapsComponent, LayersDirective, LayerDirective, Inject, Annotations } from '@syncfusion/ej2-react-maps';
import * as ReactDOM from 'react-dom';

const SAMPLE_CSS = `
    .control-fluid {
    padding: 0px !important;
    }
    #annotation {
        color: #DDDDDD;
        font-size: 12px;
        font-family: Roboto;
        background: #3E464C;
        margin: 20px;
        padding: 10px;
        -webkit-border-radius: 2px;
        -moz-border-radius: 2px;
        border-radius: 2px;
        width: 300px;
        -moz-box-shadow: 0px 2px 5px #666;
        -webkit-box-shadow: 0px 2px 5px #666;
        box-shadow: 0px 2px 5px #666;
    }`;
class App extends React.Component {
  render() {
    return (
      <div className="control-pane">
        <style>{SAMPLE_CSS}</style>
        <div className="control-section row">
          <MapsComponent id="element"
            annotations={[
              {
                content: '#maps-annotation',
                x: '0%',
                y: '70%'
              }
            ]}
          >
            <Inject services={[Annotations]} />
            <LayersDirective>
              <LayerDirective shapeData={africa_continent} />
            </LayersDirective>
          </MapsComponent>
        </div>
        <div id="maps-annotation" style={{ display: 'none' }}>
          <div id="annotation">
            <div
              style={{ marginLeft: '10px', fontSize: '13px', fontWeight: 500 }}
            >
              <h5 style={{ marginLeft: '40px' }}>Facts about Africa</h5>
            </div>
            <hr />
            <div>
              <ul style={{ listStyleType: 'disc' }}>
                <li>
                  Africa is the second largest and second most populated
                  continent in the world.
                </li>
                <li style={{ paddingTop: '5px' }}>
                  Africa has 54 sovereign states and 10 non-sovereign
                  territories.
                </li>
                <li style={{ paddingTop: '5px' }}>
                  Algeria is the largest country in Africa, where as Mayotte is
                  the smallest.
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('maps'));

```

{% endtab %}